---
sidebar_position: 3
---

# Process of setting up the experiment

Sometimes it's useful to think about the experiments overall, about the process of implementing new experiments in your product. Based on that process quality level you will have the level of quality for your final results.

1. Define the hypothesis of the improvement, and what feature you can improve. For example, you want to test the color of the purchase button
2. Define the multiple variables of the improvement. For the button, it will be "gray", "red", and "blue" for example. Currently, the color of the button is orange.
3. Create the experiment in the ABRouter dashboard with the name "Purchase button color", uid: "purchase_button_color", and with the following branches: gray, red, blue, original (orange, current color). The split between branches will be 25/25/25/25.
4. Set up the ABRouter in your project. See the available SDKs
5. Define the events to track in your app and start sending them to ABRouter statistics.
6. Implement the behavior on the running experiment in your product codebase. After a run, the application will receive the branch name. Based on that you have to change your application regarding the branch.
7. Wait for enough data in the statistics to make a decision. Time-to-time checks the statistics to see the impact on your OKR metrics. If experiment branches are losing, time to think about stopping and reworking the experiment.
8. After receiving enough data it's time to make the decision. Choose the right branch to make it a behavior.
9. Deploy experiment removal
10. Remove the experiment from ABRouter.
