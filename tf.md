# tf

### tf_test

```python
import matplotlib.pyplot as plt
import numpy as np

# Draw samples from a uniform distribution(low=0.0, high=1.0, size=None)
observations = 1000
xs = np.random.uniform(low=-10, high=10, size=(observations, 1))
zs = np.random.uniform(-10, 10, (observations, 1))

inputs = np.c_[xs, zs]  # concatenate/columns

# Create a new figure, or activate an existing figure
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(xs.reshape(observations, ), zs.reshape(observations, ),
        targets.reshape(observations, ))  # 输入参数转成1维
ax.set_xlabel('xs')
ax.set_ylabel('zs')
ax.set_zlabel('Targets')
ax.view_init(azim=100)  # 可视化
plt.show()
```

### tf_01

```python
import matplotlib.pyplot as plt
import numpy as np
import tensorflow as tf
# savez(file, *args, **kwds)
np.savez("./np_data/TF_intro", inputs=generated_inputs,
         targets=generated_targets)
training_data = np.load("./np_data/TF_intro.npz")

model = tf.keras.Sequential()
model.add(tf.keras.layers.Dense(output_size,
                                # Initializer for the kernel weights matrix
                                kernel_initializer=tf.random_uniform_initializer(minval=-0.1, maxval=0.1),
                                # Initializer for the bias vector
                                bias_initializer=tf.random_uniform_initializer(-0.1, 0.1)))
custom_optimizer = tf.keras.optimizers.SGD(learning_rate=0.02)
model.compile(optimizer=custom_optimizer, loss="mean_squared_error")
model.fit(training_data["inputs"], training_data["targets"],
          epochs=100, verbose=0)
weights = model.layers[0].get_weights()[0]
bias = model.layers[0].get_weights()[1]

# predict will go through all the data, batch by batch, predicting labels
# predict_on_batch, on the other hand, assumes that the data you pass in
# is exactly one batch and thus feeds it to the network
outputs = model.predict_on_batch(training_data["inputs"]).round(1)  # 2D, round为四舍五入函数
targets = training_data["targets"].round(1)  # 2D
plt.plot(outputs, targets)
plt.xlabel("outputs")
plt.ylabel("targets")
plt.show()
```

### tf_mnist

```python
import tensorflow as tf
import tensorflow_datasets as tfds

# 加载数据
mnist_dataset, mnist_info = tfds.load(name='mnist', with_info=True, as_supervised=True)
num_validation_samples = 0.1 * mnist_info.splits['train'].num_examples  # 内部属性
# Casts a tensor to a new type
num_validation_samples = tf.cast(num_validation_samples, tf.int64)
def scale(image, label):
    image = tf.cast(image, tf.float32)
    image /= 255.
    return image, label


# 训练集测试集都进行图片范围转化
scaled_train_and_validation_data = mnist_train.map(scale)
# 将训练集洗牌，将前面一部分拿出来做验证集，构建训练集和验证集
BUFFER_SIZE = 10000
shuffled_train_and_validation_data = scaled_train_and_validation_data.shuffle(BUFFER_SIZE)
validation_data = shuffled_train_and_validation_data.take(num_validation_samples)
train_data = shuffled_train_and_validation_data.skip(num_validation_samples)

# 将训练集分成100份，验证集和测试集只分成1份（即不分）？
BATCH_SIZE = 100
train_data = train_data.batch(BATCH_SIZE)
validation_data = validation_data.batch(num_validation_samples)
test_data = test_data.batch(num_test_samples)

# 将验证集通过迭代分成了输入与输出，这意味着我们加工后的数据本身是可迭代的？
validation_inputs, validation_targets = next(iter(validation_data))
```

### tf_audiobook

```python
import pandas as pd
from imblearn.over_sampling import SMOTE
from sklearn import preprocessing
import tensorflow as tf

# pandas初始化设置
pd.set_option('display.max_columns', 1000)
pd.set_option('display.width', 1000)
pd.set_option('display.max_colwidth', 1000)

X_resampled, y_resampled = SMOTE().fit_resample(X, y)  # 过采样
X_scaled = preprocessing.scale(X_resampled)  # 正则化，X会转变成ndarray

# early_stopping
early_stopping = tf.keras.callbacks.EarlyStopping(patience=2)
model.fit(train_inputs,
          train_targets,
          batch_size=batch_size,
          epochs=max_epochs,
          callbacks=[early_stopping],
          validation_data=(validation_inputs, validation_targets),
          verbose=2)
```

### tf_audiobook_01

```python
import numpy as np

# Return a new array with sub-arrays along an axis deleted. 
'''examples
arr = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
np.delete(arr, np.s_[::2], 1)
'''
unscaled_inputs_equal_priors = np.delete(unscaled_inputs_all, indices_to_remove, axis=0)
np.random.shuffle(shuffled_indices)  # 将索引洗牌

npz = np.load('./np_data/audiobook_train_01.npz')
train_inputs = npz['inputs'].astype(np.float)  # astype
```

# deeplearning_ai

## course_01

