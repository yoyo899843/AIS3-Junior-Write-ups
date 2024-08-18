# �P��GPT�x�]�O�a
�L���ڭ̳Q�[�K���r��A���ڭ̷�M�N�o�ѱK�աA���O~~�����s��~~���|python��ϦV����O? ���N��GPT�a
![alt text](image.png)

![alt text](image-1.png)
### �ӴΤF�A~~�H��CTF��python���浹�A�F GPT~~

# AI ���Фj�v
�ݨ�flag�֩w�O�@�D��
![alt text](image-2.png)
### �ܻ�flag�u���n�n�Y

# AI �i������
![alt text](image-3.png)
�]���L�|����flag��X�A�]���n�y�L�ഫ�@�Uflag

�ڥH��i�����ӳ��g�o�ܦn

![alt text](image-5.png)

# AI Markdown �峹½Ķ
��SRF����k�N�i�H���\�F
![alt text](image-6.png)

# �ƾ�����?
![alt text](image-7.png)
�L���L�i�H����python�A���N���L�h���}flag�a

# �߿߽u�W�ӫ~�M�d
![alt text](image-8.png)
�ӻŤFSQL�]�ӤF�A�N��sql�y�k�a

# FGSM
```
import tensorflow as tf
import numpy as np
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.applications.mobilenet_v2 import preprocess_input, decode_predictions
from tensorflow.keras.preprocessing import image
import matplotlib.pyplot as plt
import os

# ���J�w�V�m�� MobileNetV2 �ҫ�
model = MobileNetV2(weights='imagenet')

# ���J�ùw�B�z�����Ϥ�
img_path = 'dog.jpg'  # �д������A�����Ϥ����|
img = image.load_img(img_path, target_size=(224, 224))
x = image.img_to_array(img)
x = np.expand_dims(x, axis=0)
x_orig = x.copy()  # �O�s�@����l�Ϥ��ƾ�
x = preprocess_input(x)

# �����l�w��
original_pred = model.predict(x)
print("Original prediction:", decode_predictions(original_pred, top=1)[0])

# �]�w�ؼ����O�]�ߡ^
target_class = 281  # ImageNet ���ߪ����O����

# �w�q���N FGSM �������
@tf.function
def i_fgsm_attack(image, label, epsilon, num_iterations, alpha):
    image = tf.convert_to_tensor(image)
    adv_image = tf.identity(image)
    for _ in range(num_iterations):
        with tf.GradientTape() as tape:
            tape.watch(adv_image)
            prediction = model(adv_image)
            target = tf.one_hot(label, 1000)
            loss = -tf.keras.losses.categorical_crossentropy(target, prediction)
        gradient = tape.gradient(loss, adv_image)
        signed_grad = tf.sign(gradient)
        adv_image = adv_image + alpha * signed_grad
        adv_image = tf.clip_by_value(adv_image, image - epsilon, image + epsilon)
        adv_image = tf.clip_by_value(adv_image, -1, 1)  # �T�O�b�w�B�z�᪺�d��
    return adv_image

# �������
epsilon = 0.1  # �A�i�H�վ�o�ӭ�
num_iterations = 10  # ���N����
alpha = epsilon / num_iterations  # �C�����N���B��

adv_x = i_fgsm_attack(x, tf.constant([target_class]), epsilon, num_iterations, alpha)

# �w����ܼ˥�
adv_pred = model.predict(adv_x)
print("Adversarial prediction:", decode_predictions(adv_pred, top=1)[0])

# �Ыؿ�X�ؿ�
output_dir = 'adversarial_output'
os.makedirs(output_dir, exist_ok=True)

# �O�s��l�Ϥ�
original_output_path = os.path.join(output_dir, 'original_dog.png')
image.save_img(original_output_path, x_orig[0].astype('uint8'))
print(f"Original image saved to {original_output_path}")

# �O�s��ܼ˥�
adv_output_path = os.path.join(output_dir, 'adversarial_dog_as_cat.png')
adv_img = tf.keras.preprocessing.image.array_to_img(adv_x[0])
adv_img.save(adv_output_path)
print(f"Adversarial image saved to {adv_output_path}")

# ��ܭ�l�Ϥ��M��ܼ˥�
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.imshow(x_orig[0].astype('uint8'))
plt.title("Original Dog Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(tf.keras.preprocessing.image.array_to_img(adv_x[0]))
plt.title("Adversarial Image (Dog as Cat)")
plt.axis('off')

plt.savefig(os.path.join(output_dir, 'comparison.png'))
plt.show()

# �p���Z�ʶq
perturbation = np.abs(x - adv_x.numpy()).mean()
print(f"�����Z�ʶq: {perturbation:.4f}")

# ���top-5�w�����G
top_5_original = decode_predictions(original_pred, top=5)[0]
top_5_adversarial = decode_predictions(adv_pred, top=5)[0]

print("\nTop 5 Original Predictions:")
for i, (imagenet_id, label, score) in enumerate(top_5_original):
    print(f"{i+1}: {label} ({score:.2f})")

print("\nTop 5 Adversarial Predictions:")
for i, (imagenet_id, label, score) in enumerate(top_5_adversarial):
    print(f"{i+1}: {label} ({score:.2f})")

# �O�s�w�����G����
with open(os.path.join(output_dir, 'prediction_results.txt'), 'w') as f:
    f.write("Top 5 Original Predictions:\n")
    for i, (imagenet_id, label, score) in enumerate(top_5_original):
        f.write(f"{i+1}: {label} ({score:.2f})\n")
    f.write("\nTop 5 Adversarial Predictions:\n")
    for i, (imagenet_id, label, score) in enumerate(top_5_adversarial):
        f.write(f"{i+1}: {label} ({score:.2f})\n")
    f.write(f"\n�����Z�ʶq: {perturbation:.4f}")

print(f"\nAll results have been saved to the '{output_dir}' directory.")
```
![alt text](image-9.png)
����epsilon=0.1�ɪ��ƾ�
![alt text](image-10.png)
����epsilon=0.3���ƾ�
epsilon�ƭȶV�j�AAI�V�e���Q���F�A���O�H���o��e���ݥX��