[60分钟快速入门 PyTorch - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/66543791)
[PyTorch](https://pytorch.org/)
[浅谈 PyTorch 中的 tensor 及使用 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/67184419)
[PyTorch 的 Autograd - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/69294347)

[The Fundamentals of Autograd — PyTorch Tutorials 2.2.1+cu121 documentation](https://pytorch.org/tutorials/beginner/introyt/autogradyt_tutorial.html)

netscope: 网络结构可视化

##  torch

```python
# 创建一个张量 
torch.tensor() # e.g. torch.tensor([1,2,3])
torch.zeros()
torch.empty() # 定义未初始化的变量
torch.rand()

# 从已有张量创建
tensor.new_ones() # e.g. tensor2 = tensor1.new_ones(5,3,dtype = torch.double) 保留tensor1中的一些属性
torch.randn_like() # e.g. tensor3 = torch.randn_like(tensor2, dtype=torch.float) 保留tensor1的形状

# 张量的操作
tensor.size() -> Tuple # 获取尺寸
tensor.view() # 同numpy的.reshape()
tensor.t() # 转置
tensor[] # 访问,同numpy
tensor.item() # 获取元素(只有一个元素时)
tensor.item() # 返回数值
tensor.tolist() # 返回<list>

# 当对元素的操作函数有'_'后缀时,则会改变原张量
# 例子如下
tensor.t_() # 转置时也改变tensor

# tensor与numpy互化
tensor.numpy() -> numpy # tensor->numpy 两者公用一个内存空间
torch.from_numpy(numpy_array) # numpy->tensor

# cuda 张量
torch.cuda.is_available()->bool # 是否可用cuda
device = torch.device('cuda') # 创建cuda设备对象
torch.zeros((1,3), device = device) # 在创建tensor时放入cuda
tensor = tensor.to(device) # 传入cuda .to(device, torch.double) to也可用于改变数据类型
tensor = tensor.to('cuda') # 传入cuda
# cpu 张量同理
```
------
```python
# 张量的grad
# tensor.requires_grad # 查看是否求导
# 启用grad
torch.ones((3,3), requires_grad = True) # 在创建tensor时设置，默认False
tensor.requires_gradn = True # 直接设置
# torch.nn 中也类似，举例如下
net = torch.nn.Conv2d(3,16)
for param in net.parameters():
    param.requires_grad = False
# 当包裹在 with torch.no_grad() 中时，会暂时不更总网络参数的导数
with torch.no_grad():
    pass

# 反向传播(backward())计算梯度
tensor.backward()
# tensor梯度可以在backward()后用tensor.grad()获取
tensor.backward()
tensor.grad()

# 梯度重置/清零
tensor.zero_grad()
optimizer.zero_grad() # 也可用于optimizer

# 当backward()后改变原来计算图上的值，会导致报错

# tensor.detach() 要善用
tensor2 = tenser1.detach() # 则tensor2 requires_grad = False
```

-----

```pyt
# 常见框架
class NeuralNetwork(nn.Module):
    def __init__(self):
        super().__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28*28, 512),
            nn.ReLU(),
            nn.Linear(512, 512),
            nn.ReLU(),
            nn.Linear(512, 10),
        )

    def forward(self, x):
        x = self.flatten(x)
        logits = self.linear_relu_stack(x)
        return logits
 
 # 常用api
 nn.flatten()
 nn.Sequential()
 nn.Liner()
 nn.ReLu()
 nn
 
 net.to(device)
 net.parameters()
 layer.weight
```

# 遇到的操作

```python
nn.Flatten()
torch.optim.SGD()
torch.argmax()
tensor.max()
optimizer.zero_grad()
tensor.backward()
optimizer.step()
tensor.gather()
module.state_dict()
module.load_state_dict()
module.parameters()
optimizer.param_groups()
torch.save(model.state_dict(), 'model_weights.pth')
model.load_state_dict(torch.load('model_weights.pth'))
np.random.uniform()
np.random.choice()
一个小坑: 如果梯度上升取+号 梯度下降取-号
torch.distributions.Categorial() # 离散分布, 输入概率, 可以通过.sample()采样
```

# 注意

tensor.backward(), 中的参数[pytorch中backward()函数详解_pytorch backward-CSDN博客](https://blog.csdn.net/sinat_28731575/article/details/90342082)

torch.optim 不仅可以optim model 也可以optim grad=True的tensor

model 中hook的使用， 可以避免修改forward()函数

对moudel进行手动赋值：使用nn.Parameter(new_weight)包裹new_weight

