# Promise

## 创建`Promise`的方法

```javascript

// 传入一个excutor
var promise1 = new Promise( (resolve, reject) => {
	if(success){
		resolve(value);
	}else{
		reject(reason);
	}
} );

var promise2 = promise1.then(fullfillment, rejection);

```

需要注意的是：

- `Promise`就是一个过程在未来的状态：`Fullfilled`或者`Rejected`。

- `Promise`状态(Pending[default], Fullfilled, Rejected)的设置:
	+ 执行`resolve`会将`Promise`对象置为`Fullfilled`。
	+ 执行`reject`会将`Promise`对象置为`Rejected`。
	+ 在excutor执行过程中抛出异常，`Promise`对象置为`Rejected`。
- `Promise`对象一旦被定为某种状态，那么就再也无法改变。也就是说，一旦执行了`resolve`或`reject`只能执行一次，再次执行不再会改变状态。

- `Promise.prototype.then()`返回的是一个新的`Promise`对象。
	+ 接受两个参数：`fullfillment`和`rejection`。
		* 如果调用这个`then`方法的`Promise`对象是`Fullfilled`状态，那么就调用`fullfillment`。
		* 如果调用这个`then`方法的`Promise`对象是`Rejected`状态，那么就调用`rejection`。
	+ 返回一个新的`Promise`对象，这个对象的状态：
		* 执行`fullfillment`为`Fullfilled`。
		* 执行`rejection`置为`Rejected`。
		* 在执行过程中抛出异常，`Promise`对象置为`Rejected`。
- `Promise.prototype.catch()`相当于`Promise.prototype.then(null, rejection)`。

- 在**链式调用**的过程中，数据(value)或错误原因(reason)的传递：
	+ 最早的`Promise`对象调用`resolve(value)`，其中的`value`会传递给在`then`中的`fullfillment(value)`。
	+ 最早的`Promise`对象调用`reject(reason)`或抛出一个异常，其中的`reason`或错误会传递给在`then`或`catch`中的`rejection(reason)`。

- 在**链式调用**的过程中，也可以传递`Promise`对象：
	+ 包括：在excutor中`resolve()`或`reject()`传入的`Promise`对象；以及在`then`和`catch`中返回的`Promise`对象
	+ 如果传入或返回的`Promise`对象是在`resolve`或者`fullfillment`中出现，那么调用该方法的`Promise`对象的状态就是传入的这个`Promise`对象的状态结果(阻塞，Blocking)：
		* 如果是`Fullfilled`，那么最早的`Promise`对象也会被置为`Fullfilled`。
		* 如果是`Rejected`，那么最早的`Promise`对象也会被置为`Rejected`。
	+ 如果传入或返回的`Promise`对象是在`reject`或者`rejection`中出现，那么调用该方法的`Promise`对象的状态就会立即改为`Rejected`，传入的`reason`就是`Promise`对象。

- 如果已经确定`Promise`对象的状态会是`Fullfilled`，可以使用`Promise.resolve(value)`，类似的`Promise.reject(reason)。

- 多个`Promise`对象：
	+ `Promise.all`：所有的`Promise`对象的状态均以改变。只要有一个`Rejected`，返回的`Promise`对象就是`Rejected`
	+ `Promise.race`：只要有一个`Promise`的状态改变