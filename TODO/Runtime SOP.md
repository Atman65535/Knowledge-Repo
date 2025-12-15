# BUILD Attention Pipeline

1. DDIM reverse.
	1. build uncond embed and prompt embed
	2. CFG denoise
	3. reverse to several steps before.
	4. return latent.
2. Hijack U-Net
	1. build hijack method. Rewrite attention flow
	2. find all children node with `__class__.__name__ == "Attention"`
	3. replace their forward method with hijack method
	4. update counter. Finally get a counter of overall replacement.
	5. finish hijack, remember to release it
3. get attention map
	1. make out the shape stored in your attention controller.
	2. specify which size you want
	3. get that maps and average them.
	4. get cross attention map, loss is its variance
4. release hijack
	1. change the forward function in step 3 and apply it to U-Net again.
5. calculate loss.
	1. loss = - classify cross entropy loss + self attention MSE loss + cross loss

>[!bug] INVARIANTS
>don't run whole code before validate each small part.
>write a minimum test code in each file.
>



## Main Pipeline BUILD CARD

### Step 1: Build Rellis3D Data Loader

### Step 2: classifier predict
- preprocess image batch, get class_image
- cross entropy loss

### Step 3: Attention Attack
- set loss variable: self attn loss and cross attn loss = 0
- for image in batch, Attention Attack.
	- input: image, \[B, C, H, W], RGB, range from \[-1, 1]
	- return two loss. Add to loss variable in procedure above.
- loss.backward()
- optim.step()
- optim.zero_grad.
## Attention Attack BUILD CARD (DO NOT THINK)

### Step 0: Basic Utils
- vae_encoder
	- set random seeds
	- encode image
	- return 
- diffusion image checker
	- check ndim = 4
	- check CHW valid
	- if `strict`, check range -1, 1
>[!warning] RBG or BGR!
>- [ ] check input is RGB !
### Step 1: DDIM Reverse
- check image shape, range and channel.(CHW, RGB)
- build uncond + prompt embed
- CFG denoise
- reverse N steps
- RETURN latent

### Step 2: Hijack U-Net
- find modules: class name == Attention
- replace forward with hijack
- record count
- ASSERT count > 0

### Step 3: Attention Map
- get stored attention tensor
- select predefined size
- average maps
- cross-attn variance → cross loss

### Step 4: Release Hijack
- restore original forward
- ASSERT no hijack remains

### Step 5: Loss
loss = - CE + self-attn MSE + cross-attn loss

>[!tip] HARD INVARIANTS
> - Each file must have a runnable __main__ test
> - No full pipeline run before each part passes


# Next day boot 
1. finish ddim reverse. 
2. push that pipeline.