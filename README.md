PINN for Solving the Diffusion Equation
Table of Contents
Introduction
Diffusion Equation
Model Architecture
Loss Functions
Training Process
Initial and Boundary Conditions
Visualization
Usage
License
Introduction
This repository contains a Python implementation of a Physics-Informed Neural Network (PINN) to solve the diffusion equation. The diffusion equation describes how the concentration of a substance changes over time and space, often used in various fields such as physics, chemistry, and biology.

Diffusion Equation
The diffusion equation can be expressed as:

∂
𝑢
∂
𝑡
=
𝐷
∂
2
𝑢
∂
𝑥
2
+
𝑓
(
𝑥
,
𝑡
)
∂t
∂u
​
 =D 
∂x 
2
 
∂ 
2
 u
​
 +f(x,t)
where:

𝑢
(
𝑥
,
𝑡
)
u(x,t) is the concentration of the substance at position 
𝑥
x and time 
𝑡
t.
𝐷
D is the diffusion coefficient.
𝑓
(
𝑥
,
𝑡
)
f(x,t) is an external source term that represents additional influences on the concentration.
In this implementation, we simplify the equation by assuming a constant diffusion coefficient 
𝐷
=
0.01
D=0.01 and neglecting the external source term 
𝑓
(
𝑥
,
𝑡
)
f(x,t).

Model Architecture
The model consists of three fully connected layers with 20 neurons each, using the hyperbolic tangent activation function. The architecture is defined in the PINN class:

python
Copy code
class PINN(tf.keras.Model):
    def __init__(self):
        super(PINN, self).__init__()
        self.dense1 = tf.keras.layers.Dense(20, activation='tanh')
        self.dense2 = tf.keras.layers.Dense(20, activation='tanh')
        self.dense3 = tf.keras.layers.Dense(1)  # Output layer
Loss Functions
The model incorporates three types of loss functions to train the neural network:

PDE Loss: Measures the deviation from the diffusion equation.
Boundary Loss: Ensures the model adheres to specified boundary conditions.
Initial Loss: Ensures the model adheres to the initial condition.
The total loss is computed as follows:

python
Copy code
def compute_loss(model, x, t, x_boundary, t_boundary, x_initial, u_initial, t_initial):
    pde_loss = loss_pde(model, x, t)
    boundary_loss = loss_boundary(model, x_boundary, t_boundary)
    initial_loss = loss_initial(model, x_initial, t_initial, u_initial)
    total_loss = 10 * pde_loss + boundary_loss + initial_loss  # Adjust weights
    return total_loss
Training Process
The training process uses an Adam optimizer with a learning rate schedule to minimize the total loss over a specified number of epochs:

python
Copy code
optimizer = tf.keras.optimizers.Adam(learning_rate=lr_schedule, clipvalue=1.0)

def train_pinn(epochs=100):
    model = PINN()
    for epoch in range(epochs):
        loss = train_step(model, x_train, t_train, x_boundary, t_boundary, x_initial, u_initial, t_initial)
        if epoch % 100 == 0:
            print(f"Epoch {epoch}: Loss = {loss.numpy()}")
    return model
Initial and Boundary Conditions
In this implementation, the following conditions are applied:

Initial Condition: The initial concentration profile is set as 
𝑢
(
𝑥
,
0
)
=
sin
⁡
(
𝜋
𝑥
)
u(x,0)=sin(πx).
Boundary Conditions: Random values are assigned for the boundary conditions.
These conditions are crucial as they provide the necessary constraints for the model to learn the underlying physical phenomena.

Visualization
The model provides two visualization functionalities:

Fixed Time Plot: Displays the solution 
𝑢
(
𝑥
,
𝑡
)
u(x,t) for a specific time 
𝑡
t.
Animation: Animates the evolution of the solution over time.
python
Copy code
def plot_fixed_time(model, t_val):
    # Visualization code...
    
def animate_solution(model):
    # Animation code...
Usage
To use this implementation:

Ensure you have the required libraries:

bash
Copy code
pip install numpy tensorflow matplotlib
Run the main script to train the model and visualize the results:

python
Copy code
# Example data initialization and model training
model = train_pinn(epochs=1000)
plot_fixed_time(model, t_val=0.5)
animate_solution(model)
License
This project is licensed under the MIT License. See the LICENSE file for details.
