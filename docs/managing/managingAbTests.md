---
sidebar_position: 1
---

# Managing and creating feature flags

## Creating
Important things in the experiment are experiment uid and branches. Experiment uid will be used in the code of your project to identify the experiment. Branches are the percentage to control the spreading of the users into testing variables.
Let's do it step by step:

Login to your account

Click "Create new experiment"

Imagine experiment name:
The experiment name is your internal title of the experiment. You don't have to use it in your code.

Imagine experiment uid:
Experiment uid will be used to identify the experiment in your code.

Branches:
Now, you have to define the branches, and the splits(percentages) for each branch, that will be used for spreading your users into the branches. The branch, that the user got will define what he will see or experience in your product.
Relying on the branch you have to create the "if-statement" in your app to apply the experiment to the application behavior.

Then, click "Create" to save the data. You can edit it any time except the experiment uid. After creating the experiment will appear in your dashboard. You can copy the Experiment ID to use in your application.

## Editing experiment
To edit the experiment, find it in your dashboard and click on the pencil icon. You can easily change the percentage splits to raise the number of users who will get into some branches. It's highly recommended to set up the lower split to the branch which will probably affect your revenue and user experience. Then, based on the data you can raise the percentage if you see the sales/revenue growth in that branch.

## Deleting the experiment
If you already running the experiment in the application we highly don't recommend you delete that branch. It will not break your application, but can probably affect something. So, be careful and delete your experiment if you are sure the experiment is not used in your app yet or anymore.
