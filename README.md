# pytorch

[TOC]

中文:
https://pytorch-cn.readthedocs.io/zh/latest/

https://speech.ee.ntu.edu.tw/~hylee/ml/2022-spring.php

## DataSet

torch.Dataset: 原始資料定義好輸入輸出
torch.Dataloader: group資料與multiprocess

```python=
dataset = Mydataset(file)
dataloader = DataLoader(dataset,batchsize,shuffle=True)
```

1. 讀取data與前處理 ()
2. 回傳一個sample一個時間
3. 資料大小

![](https://i.imgur.com/qawxrmk.png)

在從np輸入進去模型最好先轉成float32

```python=
x = x.astype(np.float32)
```

label 轉成longtensor
```
self.targets =  torch.LongTensor(targets)
```

https://pytorch.org/tutorials/beginner/data_loading_tutorial.html

在 PyTorch 中，我們可以利用 torch.utils.data 的 Dataset 及 DataLoader 來"包裝" data，使後續的 training 及 testing 更為方便。

Dataset 需要 overload 兩個函數：\_\_len\_\_ 及 \_\_getitem\_\_

\_\_len\_\_ 必須要回傳 dataset 的大小，而 \_\_getitem\_\_ 則定義了當程式利用 [ ] 取值時，dataset 應該要怎麼回傳資料。

實際上我們並不會直接使用到這兩個函數，但是使用 DataLoader 在 enumerate Dataset 時會使用到，沒有實做的話會在程式運行階段出現 error。

```python=
from torch.utils.data.dataset import Dataset

class customDataset(Dataset):
    def __init__(self):
        # --------------------------------------------
        # Initialize paths, transforms, and so on
        # --------------------------------------------
        
    def __getitem__(self, index):
        # --------------------------------------------
        # 1. Read from file (using numpy.fromfile, PIL.Image.open)
        # 2. Preprocess the data (torchvision.Transform).
        # 3. Return the data (e.g. image and label)
        # --------------------------------------------
        
    def __len__(self):
        # --------------------------------------------
        # Indicate the total size of the dataset
        # --------------------------------------------
```

測試dataset -- 直接分割
```python=
train_set = musicDataset("trainsample.csv",transform)

data1 = train_set[0]
print("img shape: ",data1[0].shape)
plt.imshow(data1[0].permute(1, 2, 0))
plt.show()
print("contextual : ",data1[1].shape)
print("label : ",data1[2])
```

測試dataloader -- iter
```python=
batch_size = 32
train_loader = DataLoader(train_set, batch_size=batch_size, shuffle=True)

dataiter = iter(train_loader)
i,c,l = dataiter.next()
print(i.shape)
```


### detach
NO autograd

### pin_memory
pin_memory就是鎖頁內存，創建DataLoader時，設置pin_memory=True，則意味著生成的Tensor數據最開始是屬於內存中的鎖頁內存，這樣將內存的Tensor轉義到GPU的顯存就會更快一些。

主機中的內存，有兩種存在方式，一是鎖頁，二是不鎖頁，鎖頁內存存放的內容在任何情況下都不會與主機的虛擬內存進行交換（注：虛擬內存就是硬盤），而不鎖頁內存在主機內存不足時，數據會存放在虛擬內存中。

而顯卡中的顯存全部是鎖頁內存！
```python=
train_loader = DataLoader(train_dataset,/
                      batch_size=config['batch_size'], /
                          shuffle=True, pin_memory=True)
```


## 訓練小
https://zhuanlan.zhihu.com/p/302409233

## Tensor

1. 直接建立
```python=
x = torch.tensor(array)
x = torch.from_numpy(np array)
```

2. 建立0、1
```python=
x = torch.zeros(維度)
```

3. from numpy
```python=
x = torch.from_numpy(x).float()
```
### 轉置 transpose
transpose只能二維
```
X.transpose(0,1)
```

permute多維
```
x.permete(1,0,2)
```

### 變形 view
```
x.view(16,16,-1) #shape 16,16,-1
```

view 與 permute
https://clay-atlas.com/blog/2020/07/25/pytorch-cn-how-to-convert-dimension-view-permut/

轉置 (transpose)、view、permute的差異
```python=
x = torch.tensor([[1, 2, 3], [4, 5, 6]]) # x is contiguous
y = torch.transpose(0, 1) # y is non-contiguous

#變成非連續了
print(x.is_contiguous()) # True
print(y.is_contiguous()) # False

#你可以透過呼叫 contiguous()來返回連續的tensor，不然有些操作會報錯
----

a = torch.rand(3, 4)

In [3]: id(a), id(a.storage())
Out[3]: (2236511690472, 2236511611848)

b = a.view(2, 6)

In [5]: id(b), id(b.storage())
Out[5]: (2236523527984, 2236470501128)

---
x = torch.rand(16, 32, 3)
y = x.tranpose(0, 2)

z = x.permute(2, 1, 0)
```

view會**copy**原來的數值並返回一個不同維度的tensor
transpose和view一樣會copy並返回新的tensor，但!! transpose可以**處理連續與非連續的tensor，view只能處理連續**。
非連續舉例 (noncontiguous layouts (e.g. crop a picture using indexing))

連續在pytorch的意思是tensor內所有的element在記憶體內與其他element相鄰。

permute與transpose相似，差別是transpose只能兩維度轉換，permute可以轉換多個維度

### 矩陣相乘
https://ofooo.github.io/wiki/%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD/pytorch/torch%E4%B9%98%E6%B3%95/

**$torch.mm$** 是兩個二維矩陣相乘。超過二維會報錯
```python=
mat1 = torch.randn(2,3)
print("mat1=", mat1)

mat2 = torch.randn(3,2)
print("mat2=", mat2)

mat3 = torch.mm(mat1, mat2)
print("mat3=", mat3)
```
**$torch.bmm$** 是加了batch的mm，因此相乘的兩個矩陣第一維batch必須相同

```python=
mat1 = torch.randn(10, 2, 4)
# print("mat1=", mat1)

mat2 = torch.randn(10, 4, 1)
# print("mat2=", mat2)

mat3 = torch.matmul(mat1, mat2)
print("mat3=", mat3, mat3.shape)
# (10,2,1)
```
**torch.matmul**
torch.mm仅仅是供矩阵相乘使用，使用范围较为狭窄。
1. 如果两个tensor都是一维的，则为点乘运算，即每个元素对应相乘求和

```python=
mat1 = torch.Tensor([1,2])
print("mat1=", mat1)

mat2 = torch.Tensor([1,2])
print("mat2=", mat2)

mat3 = torch.matmul(mat1, mat2)
print("mat3=", mat3)
```
![](https://i.imgur.com/ihc62Kk.png)

2. 如果两个都是二维的，那么就如同torch.mm
3. 如果第一个入参是一维的，第二个入参是二维的，则第一个参数增加一个一维，做矩阵乘法，结果然后去掉一维

如， 第一参数A shape为（2），第二参数B shape（2，2），先讲A增加一维，shape为（1，2），然后计算矩阵相乘结果为（1，2），再去掉第一维，改为（2）
```python=
mat1 = torch.Tensor([1,-1])
print("mat1=", mat1)

mat2 = torch.Tensor([[1,2],[-1,-2]])
print("mat2=", mat2)

mat3 = torch.matmul(mat1, mat2)
print("mat3=", mat3, mat3.shape)
```
![](https://i.imgur.com/i2sXN4t.png)

4. 如果第一个入参是二维的，第二个是一维，则将第二个参数扩展一维，做矩阵乘法。

如， 第一参数A shape为（2，2），第二参数B shape（2），先将B增加一维，shape为（2,1），然后计算矩阵相乘结果为（2,1），再去掉第一维，改为（2）

```python=
mat1 = torch.Tensor([[1,2],[-1,-2]])
print("mat1=", mat1)

mat2 = torch.Tensor([1,-1])
print("mat2=", mat2)

mat3 = torch.matmul(mat1, mat2)
print("mat3=", mat3, mat3.shape)
```
![](https://i.imgur.com/928CSTM.png)

5. 两边shape的rank要相同，最后两维是用来做mm计算的。如果shape的rank不同，则可以通过“broadcast”，即+1维。 如shape（10，4，2）matmul shape（2，3）则变为 shape（10，4，2）matmul shape（1，2，3）

* 如果是shape（10，4，2）matmul shape（2，2，3）会报错，因为batch不匹配
* 如果是shape(2,3, 2, 4)matmul shape(2, 4, 1)，也会报错。因为batch （2，3）不匹配 （2）
* 但是shape(2,3, 2, 4)matmul shape(3, 4, 1) 是可以的，因为 shape(3, 4, 1) 可以通过broadcast转为shape(1，3, 4, 1)

### 取代 where
好用
https://pytorch.org/docs/stable/generated/torch.where.html

## T-SNE
https://yanwei-liu.medium.com/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8pytorch%E7%9A%84feature-extractor%E8%BC%B8%E5%87%BA%E9%80%B2%E8%A1%8Ct-sne%E8%A6%96%E8%A6%BA%E5%8C%96-e3cfd7e3cfec


## autoGrad
https://pytorch.org/docs/stable/notes/autograd.html

## 訓練
### L2 regulation 
透過optimizer 的weight decay


計算梯度
```python=
x = torch.tensor([[1,0],[-1,1]],requires_grad = True)
# requires_grad 相要計算梯度

z = x.pow(2).sum()
z.backward()
x.grad
> tensor([[2,0],[-2,2]])
```
![](https://i.imgur.com/FQ2xwSq.png)

LOSS
```python=
criterion = nn.MSELoss()
loss = criterion(model_output,expected_value)
```

訓練步驟
1. optimizer.zero_grad()來reset model parameters 的gradient
2. loss.backward() 來backpropagate gradient來計算loss
3. optimizer.step()來調整模型參數

訓練
![](https://i.imgur.com/OxxuE2f.png)

測試
![](https://i.imgur.com/FYQg1Yv.png)



### forze Seed
```python=
def same_seed(seed): 
    '''Fixes random number generator seeds for reproducibility.'''
    torch.backends.cudnn.deterministic = True
    torch.backends.cudnn.benchmark = False
    np.random.seed(seed)
    torch.manual_seed(seed)
    if torch.cuda.is_available():
        torch.cuda.manual_seed_all(seed)
```

### Tensorboard

```python=
# For plotting learning curve
from torch.utils.tensorboard import SummaryWriter

writer = SummaryWriter() # Writer of tensoboard.

for epoch in epochs:
  mean_train_loss
  pass
  
writer.add_scalar('Loss/train', mean_train_loss, step)
# tag,loss,step
```

open in ipynb
```
# 引用外部tensorboard (通过其模块名称重新加载IPython扩展)
%reload_ext tensorboard
%tensorboard --logdir=./runs/
```

## Model

### Testing & Val
在eval模式下，dropout層會讓所有的激活單元都通過，而batchnorm層會停止計算和更新mean和var，直接使用在訓練階段已經學出的mean和var值。

而with torch.no_grad()則主要是用於停止autograd模塊的工作，以起到加速和節省顯存的作用，具體行為就是停止gradient計算，從而節省了GPU算力和顯存，但是並不會影響dropout和batchnorm層的行為。

如果不在意顯存大小和計算時間的話，僅僅使用model.eval()已足夠得到正確的validation的結果；而with torch.no_grad()則是更進一步加速和節省gpu空間（因為不用計算和存儲gradient），從而可以更快計算，也可以跑更大的batch來測試。

```python=
predict = []
model.eval() # set the model to evaluation mode
with torch.no_grad():
    for i, data in enumerate(test_loader):
        inputs = data
        inputs = inputs.to(device)
        outputs = model(inputs)
        _, test_pred = torch.max(outputs, 1) # get the index of the class with the highest probability

        for y in test_pred.cpu().numpy():
            predict.append(y)
```


### Classifier
Loss 是batch的平均
```python=
for x,y:
  batch_loss = criterion(outputs, labels)
  _, train_pred = torch.max(outputs, 1)
  #...
  train_acc += (train_pred.cpu() == labels.cpu()).sum().item()
  train_loss += batch_loss.item()
  
print('[{:03d}/{:03d}] Train Acc: {:3.6f} Loss: {:3.6f}'.format(
    epoch + 1, num_epoch, train_acc/len(train_set), train_loss/len(train_loader)
    ))
```


### Save & Load
保存成ckpt檔，是保存參數而不是模型全部
![](https://i.imgur.com/hD0TXb2.png)

```python=
torch.save(model.state_dict(), config['save_path']) # Save your best model

# Load Model
model = My_Model(input_dim=x_train.shape[1]).to(device)
model.load_state_dict(torch.load(config['save_path']))
```

### 特點
在conv上用batchnorm，在linear上用dropout
```python=
nn.Conv2d(3,16,3,1,1), 
nn.BatchNorm2d(16),
nn.ReLU(),
nn.MaxPool2d(2,2,0), 

nn.Linear(1024, 128),
nn.ReLU(),
nn.Dropout(0.5),
```
