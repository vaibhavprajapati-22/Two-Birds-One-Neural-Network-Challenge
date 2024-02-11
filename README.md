# Two-Birds-One-Neural-Network-Challenge
In this problem, it is required that the function vector X0 be a decreasing straight line and X1 be an increasing straight. The functions Y0 and Y1 are given. The goal is to generate a complete solution space of combination (X0, X1) simultaneously satisfying functions Y0 and Y1. The solution space should be as diverse as possible and be generated by a generative model.

![image](https://github.com/vaibhavprajapati-22/Two-Birds-One-Neural-Network-Challenge/assets/148644657/544b5be3-e7ed-4838-9dff-5cba007cb22a)

# Solution Description

For this problem I have used CVAE Models to generate more samples for the given condition of y1 and y2. The Architecture of the model has been slightly changed from starter notebook provided by the DSG. According to the blog post https://agustinus.kristia.de/techblog/2016/12/17/conditional-vae/ the encoder model should input x0 and x1 as well the given y1 and y2 conditions during training. Sampling Model is same. Decoder Model have inputs for Z(Got from Sampling Model) and y1 and y2 for generating x0_hat and x1_hat.

![image](https://github.com/vaibhavprajapati-22/Two-Birds-One-Neural-Network-Challenge/assets/148644657/417e4daf-99a6-4cd2-84d8-85cafbde5300)

Loss function has three components x_loss, y_loss and KL Divergence loss. x_loss and y_loss measures mean absolute difference between actual value and predicted value.

x_loss measures error between (x0_x1) and (x0_x1_hat) while y_loss measures error between (y1_y2) and (y1_y2_hat). We get (y1_y2_hat) by putting the values of (x0_x1_hat) in the function provided to us. 

By decreasing x_loss we try to make predicted (x0_x1_hat) values to be linear and close to (x0_x1). By decreasing y_loss we try change the values of predicted (x0_x1_hat) in such a way that we get (y1_y2_hat) closer to (y1_y2).

By decreasing KLD loss we are trying to make the distribution of latent sample space to be standard normal distribution.

The goal is to strike a balance between fitting the data well (reconstruction error) and regularizing the latent space (KLD term).

# Problems Faced

- Traning the model for large number of epochs(i.e. 100) then for a given values of y1 and y2 we start to get same values of x0_x1_hat every time we fed y1 and y2. Instead we should get different values of x0_x1_hat every time as we are sampling z from the Sampling Model.
- 
- There is trade off between x_loss and y_loss if we try to minimize one we can see effect on the other one also. When we try to decrease the x_loss the model start predicting the values that are almost linear and close to x0_x1 but sson the model starts to overfit.

# Setup 
![image](https://github.com/vaibhavprajapati-22/Two-Birds-One-Neural-Network-Challenge/assets/148644657/373081ba-0da0-4d00-ba8b-97115a923259)

# References
- https://towardsdatascience.com/understanding-conditional-variational-autoencoders-cd62b4f57bf8
- https://medium.com/@sofeikov/implementing-conditional-variational-auto-encoders-cvae-from-scratch-29fcbb8cb08f
- https://agustinus.kristia.de/techblog/2016/12/17/conditional-vae/
