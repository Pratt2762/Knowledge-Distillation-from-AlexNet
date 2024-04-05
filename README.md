# Knowledge-Distillation

In this experiment, we conduct a comparative study of three lightweight student models to observe and understand the impact of relation-based knowledge distillation from a pretrained teacher model on an image classification task with a restricted number of training epochs.

## Methodology

1. Dataset Preparation - The publicly available CIFAR-10 dataset has been chosen for the comparative study. All dataset images have first been normalized. To introduce variety in the validation set, random crop, and
random horizontal flip augmentation techniques have been used.

2. Teacher Model - The teacher model that has been chosen for the study is the AlexNet architecture. The teacher model has first been trained on our CIFAR-10 dataset for a large number of (20) epochs, till it achieves a competitive accuracy on the validation dataset. For the experiment, slight overfitting of the teacher model on the training dataset has been ignored.

3. Student Models and Architecture - Three distinct student models have been used for our study. The architecture for each of these models is the same, a simple CNN architecture comprised of two CNN blocks and three subsequent linear layers. Each CNN block comprises a convolutional layer, a batch normalization layer, ReLU activation, and a max pooling layer. Both the depth of the students’ architecture, as well as the depth of its convolutional layers, are lesser than that of the teacher model, thus lending the student models a significantly lighter footprint than that of the teacher model.

4. Knowledge Distillation Process - The three student models have been trained using the Stochastic Gradient Descent (SGD) optimizer, and a unique loss function comprised of student loss (which is given by the Cross-Entropy loss between the predictions given by a student model on a batch of input images, and their ground truth labels from the training dataset) + distillation loss (which is given by the Cross-Entropy loss between the predictions given by a student model on a batch of input images, and the predictions given by the student model on the same input batch). α is a hyperparameter that decides how much weight is to
be given to the student loss in the loss equation while training the student model. It lies in the range of 0 to 1.
The first student model has been trained with α = 1, which implies that its loss equation comprises only the student loss, and it does not make use of the teacher model in the training process. The second student model has been trained with α = 0, which implies that its loss equation comprises only the distillation loss, and it learns to only mimic the teacher model’s outputs, ignoring the ground-truth labels in the training
process. The third student model has been trained with α = 0.5, which implies that its loss equation comprises both the student loss as well and distillation loss, with equal weight given to both.

5. Evaluation - To evaluate and compare the performances of the three student models, their training loss and validation loss curves during the training process have been plotted and observed, and the final accuracies returned by each student model on the training, validation, and test set have been tabulated. The performance of each of the three student models has been compared with each other and has also been evaluated against the pre-trained teacher AlexNet model.
