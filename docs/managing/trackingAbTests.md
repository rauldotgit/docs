---
sidebar_position: 3
---

# Tracking A/B tests

After creating the experiment and integrating it into your app, the next step is tracking. Built-in ABRouter statistics allow you to effectively track the best-performing branches of your experiments and the funnel overall.

The first step on the way to track your experiment is defining your events, and starting to send the statistics to the ABRouter. You can do it by any of the ABRouter SDK's. Defining the events to track should be integrated into the process of creating new features in your product. If you don't sure track that event or not - better decide to track because you can decide to see the statistics by this event later.

See how to send the events to ABRouter statistics.

After start sending the events of the product to the ABRouter, you have to set up the display events in your statistics dashboard.

A Statistics dashboard is currently common for all experiments and overall statistics, but we plan to implement the custom dashboards with the list of events to show.

To set up the display events:

Login to your account

Click "Statistics" on the left sidebar

Click "Add events". On this page, you will see the list of events that you have created.

Then, click "Add event".

Fill in the name of the event you're sending. Then, define the type of the event. ABRouter statistics currently have only 2 event types:

## Incremental
The incremental type is used to track the funnel indicators.
For example, if your user has visited the payment page, you can send the "visit_payment_page" event. Then, set up the display event with the name "visit_payment_page" and type "Incremental".
That metric will show you the unique relationship between user and payment page visits. If you're sending this event on each page reload, statistics will show calculate those events as one(+1), because you don't need to keep into account the rest of the events.

## Summarizable
Summarizable event type representing the value of the event in numbers. It can be a purchase, refund, or something else. Each summarizable event is calculatable. The Statistics dashboard will show you the daily sum for values of those types of events.


After determining the type of event you can create the display event. After creating an event it will appear on each statistics page of our system: statistics by experiment, overall statistics.

