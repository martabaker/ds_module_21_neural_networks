# Analysis Overview
This analysis is meant to determine which neural network models would be best used to determine which applicants for grants are most likely to succeed with their goals using the following information. 

- Name
- EIN
- Application Type
- Affiliation
- Classification
- Use Case
- Organization
- Status
- Income Amount
- Special Considerations
- Ask Amount

For the models, different features were either removed or brought back. All models use the relu activator, sigmoid output, and adam optimizer.

Given issues with the initial 4 models using the specified pre-processing steps, a keras-tuner was used to try and reach the 75% accuracy target.

## Results
### Data pre-processing for Models 1 to 4 and Keras-Tuner
- Additional pre-processing was done for Models 6 to 8 that is detailed for those Models (although the target is the same for all models)

#### Target:
- Was the charity able to complete their goal with the funding?

#### Features:
- Application Type
    - Binned items with a value count under 250 into an "Other" category
- Affiliation
- Classification
    - Binned items with a value count under 300 into an "Other" category
- Use Case
- Organization
- Status
- Income Amount
- Special Considerations
- Ask Amount

#### Variables that were removed:
- Name
- EIN

### Trained Models

Network 1:
- Layers: 3
- Nodes per layer:
    1. 7
    2. 5
    3. 3
- Loss: 6433.48
- Accuracy: 0.46764
- Summary: This is the base model and fell well short of the target 75% accuracy

Network 2:
- Layers: 3
- Nodes per layer:
    1. 100
    2. 50
    3. 25
- Loss: 3596.46
- Accuracy: 0.46764
- Summary: The loss is about half of Network 1, but accuracy was not improved. Network looks to be moderately better, but still not good.

Network 3:
- Layers: 4
- Nodes per layer:
    1. 100
    2. 50
    3. 25
    4. 15
- Loss: 44524.74
- Accuracy: 0.53236
- Summary: Adding an extra layer improved the accuracy, but the loss drastically increased. 

Network 4:
- Layers: 4
- Nodes per layer:
    1. 250
    2. 150
    3. 100
    4. 50
- Loss: 32148.51
- Accuracy: 0.46764
- Summary: Despite the extra layer and additional neurons, this model looks to be the worst of the models.

Keras-Tuner Results:
- ![Results](Images/Keras_Tuner_Results.jpg)
- Loss: 0.55235
- Accuracy: 0.73259
- Summary: As expected, the Keras-Tuner provided the best model. However, even with the Keras-Tuner, the model still did not meet the 75% target. This is likely because either the Keras-Tuner needed increased neurons per layer or because the data coming into the model needed to be processed further.

Network 6:
- Pre-processing changes:
    - Removed: Status, Special Considerations
    - Binned: Affiliation, Organization, Use Case
    - Scaled: Only scaled the Ask Amount column instead of the entire DataFrame
- Layers: 4
- Nodes per layer:
    1. 350
    2. 250
    3. 150
    4. 100
- Loss: 0.61276
- Accuracy: 0.73096
- Summary: Compared to the Networks from the original notebook, this perfomed much better. It is likely that the Status and Special Considerations columns added noise that negatively impacted the networks and that the original scaling also negatively impacted the networks.

Network 7:
- Pre-processing changes:
    - Removed: Status, Special Considerations, Affiliation, Organization, Use Case
- Layers: 4
- Nodes per layer:
    1. 350
    2. 250
    3. 150
    4. 100
- Loss: 0.63924
- Accuracy: 0.62239
- Summary: This model performed worse than Network 7. As a result, it's likely that the removed features Affiliation, Organization, and Use Case provided important associations for the networks.

Network 8:
- Pre-processing changes:
    - Same as Network 7
    - Added: Names
- Layers: 4
- Nodes per layer:
    1. 350
    2. 250
    3. 150
    4. 100
- Loss: 0.55784
- Accuracy: 0.74934
- Summary: This model was the best performing model and the closest to the goal of 75% accuracy. As a result, it is likely that the Name feature provides important predictive power to determine if an organization is likely to meet their goal.


## Summary
Overall, none of the deep learning models created reached an accuracy of 75% although the last network came very close. Given how close the final model came (with the Name feature), a keras-tuner could be used to try and optimize that model.

However, given the issues with finding an accurate deep learning model, a tree-based categorical model would likely be a better predictor for whether an organization would successfully fund their goal. Tree-based models run much faster than these deep learning models and are much more explainable. While it is possible that a keras-tuner with much more expanded parameters could provide a very accurate model, the time intesity of such an endeavor is likely not worth the effort. The speed and explainability of tree-based models make them a better option for solving this problem when a number of efforts to use neural networks have already been exhausted.