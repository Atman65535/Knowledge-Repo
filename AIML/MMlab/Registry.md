>The core mechanism of MM frame work. Which make build model from config possible and contains a **type : callable** dictionary.

>[!TIPS]
>To fully understand the philosophy behind the designation of `Registry`, there are some concepts that should be taken into account: **Decorator**, **Python Callable**, **Magic Methods**

## Decorator
```python
def decorator(func:Callable):
	def wrapper(*args, **kwargs):
		before_func_call()
		retval = func(*args, **kwargs)
		after_func_call()
		return retval
		
	return wrapper
	
@decorator
def hello_world(name):
	print(f"hello_world, {name}")
```
The basic usage of decorator is just like above. It receive a callable, not only functions, but classes, instance.... then return another wrapped callable, called "decorated callable".

However, there is one thing that should take notice: **The Decorator Is Nothing But GRAMMAR CANDY**
The true outlook likes:
```python
def decorator(func:Callable):
	def wrapper():
		pass
	return wrapper
	
def my_func():
	pass
	
my_func = decorator(my_func

# then my_func became wrapper
```
so the `@decorator` is just the abbreviation of `my_func = decorator(my_func)`
> about my understanding, in python, such a weak type language, the name `my_func` can be anything, variable, function, class name, and so on. 
> **the truth of wrapper is just change the behavior of a callable.**

# Registry
registry is a class name that defined in `mmengine.registry.registry.Registry`, but we will start from other things rather than the definition of class. 

>[!THINKING]
>Take a training pipeline into account, we first define datasets, model structure, metrics, optimizer and build them, then start training. The process of building always boring and not so robust. MMengine just wrap the build process into `Register` that we can input a `dict` or `ConfigDict` or `Config` to get the callable we want. 

```python
MODELS = Registry('models')
```
Here we get an instance of Registry. Think it as a dictionary that contains some callable classes and functions you can get by calling their name. 

Contents:
- module dict, contains the correspond relationship of name and callable
- parent and children, for search for callable of name recursively.
- scope, but always no use. Just restrain the calling region. 
- location, for **lazy import** (import it only when use it)

- get() get a callable from string
- register_module() this function have two usages, but we always use one of them. 
## register a callable first
Actually, `MODElS` contains `self._module_dict = Dict[str, Type]` to store callable, when we use `@MODELS.register_module()`, the dictionary adds a new name (actually the `__name__` of the callable we defined below if we don't specify in the upper parenthesis) and the call able to dict. 

## call and build them 
In mmlab pipeline, there are a lot of code like `xxx_build`. In these function, the process always are parsing arguments from config, call the build method from a correspond `Registry` instance. Then allocate those returned callable to the higher class, such as an encoder-decoder class, contains many callables, and they are built one by one then store in some private or public variables or methods. 

>[!Note]
There are four build method (actually only one) in `mmengine.registry.build_functions`, which are used for build from config dict. Most common, we use `build_from_cfg()`

# Hooks
> [!TIPS]
> hooks are defined in runner. when building runner, there is a step for building default and custom hooks. those callable hooks are from `HOOKS` registry instance. There are 22 points for hook function calling officially.

The name describe the behavior well. The hook is a kind of functions, that can cling to some point of train pipeline and drop out swiftly. 

## define in config file
```python
default_hooks = dict(
    timer=dict(type='IterTimerHook'),
    logger=dict(type='LoggerHook', interval=50, log_metric_by_epoch=False),
    param_scheduler=dict(type='ParamSchedulerHook'),
    checkpoint=dict(type='CheckpointHook', by_epoch=False, interval=4000),
    sampler_seed=dict(type='DistSamplerSeedHook'),
    visualization=dict(type='SegVisualizationHook'))
```
just like other registry, hooks are build from config file. 

## storage and calling
the hooks are maintained by `Runner`, and there is a well sorted list for hooks. hooks have priority and calling stages. When a hook function is derived from its ancestor, it have 22 empty methods that will be called runtime. **If the methods are overridden, it will be executed runtime** 

> actually at the 22 stages, every hook is called following the priority sequence, but if the method of that stage remains empty, it will skip naturally. 

>[!Note]
>there are 9 priorities, if we don't specify, it will remains `None`in that hook. 
>The sort method is insert sort, very primitive but effective.
>So I suspect that the priority isn't that important.

