# PROJECT
- **Pipeline**
	- Iteration counter = 0
		this counter is used for gradient accumulation, we update the gradient(backward) each epoch, but we update the patch(who possesses the gradient) after several epochs such as 10.
		- [ ] finish this part, a counter in main.py
	- Data loader -> batch of image(batch size is 1 actually)
	- Patch application, add patch on one image
		with EOT transformation
		- [ ] add an EOT switch.
	- Classifier predict
	- Insert into attention pipeline
	- process loss
		`loss.backward()` is called **every iteration**
		`optimizer.step()` is called **ONLY when counter == K**
		`optimizer.zero_grad()` is called ONLY after optimizer.step()
- **Losses**
	- Classifier loss
	- Attention loss
	- L2 norm loss
## Attention Loss
this loss is just for one iteration.
- [ ] Image convert
- [ ] DDIM reverse process (with grad)
- [ ] Attention Control module
- [ ] Hijack the network, add Attention control module.
- [ ] DDIM denoise.
- [ ] get loss cross attention and self attention.
- [ ] Remove Hijack. Turn it off.
>[!danger]
> - [ ] check loss backward, optim step and grad zero.
> - [ ] check image range [-1, 1] in diffusion pipeline
> - [ ] check RGB and CHW in classifier and diffusion pipeline.
> - [ ] **REMOVE** hijack after attention map calculation.
> - [ ] print three kinds of loss separately.
> - [ ] check gradient enable at ddim reverse
> - [ ] check gradient flow of denoise process

>[!tip] Failure Classification
> *IF* loss doesn't change
> 	- check grad flow
> 	- check hijack hook
> 	- check requires_grad
> *IF* patch doesn't update
> 	- check gradient zero 
> 	- check loss backward
> 	- check counter update



## Utilities
- [ ] register model