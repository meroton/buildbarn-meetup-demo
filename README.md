# Buildbarn Meetup 2026 - bb-portal interactive demo

Welcome to our interactive demo of bb-portal. In this demo you will build small example projects on one of our demo
clusters, and use bb-portal to solve common problems in Bazel builds.

> [!IMPORTANT]
> Please don't overload our cluster. It's a small demo cluster that probably has less performance than you laptop.

## Setup

Before starting, you will need an account for our build cluster. All accounts and all user data will be deleted shortly
after the presentation, requiring no action from you.

To create an account, navigate to <https://buildbar.meroton.com> and follow the login flow.

## Tasks

Here are a few tasks that can be done to showcase the capabilities of bb-portal.

### Why is my build taking so long?

The target `:do_something_useful` is taking too long to build. We want to see if there are any actions on the critical path
that we can improve. Use the invocation profile to find the cause of the slow build.

1. Run `bazel build //:do_something_useful --noremote_accept_cached`
2. Open the invocation in bb-portal by clicking the link in the invocation log.
3. Use the critical path visualization to determine which action is slowing the build.
4. (Optional) Open the invocation profile in Perfetto to show the entire profile.
5. Find and fix the code responsible for the slow execution.

### Compare actions

For some reason, `//:test_compare_actions` is never cached and produces a different result every time. Use the Compare
Actions feature to determine why these actions differ.

1. Run `bazel build //:test_compare_actions` twice to produce two different actions.
2. Navigate to the operations list and find the two `:test_compare_actions` operations. Open both their actions in separate
   tabs. If you cannot find your actions due to many actions running simultaneously, use the links to the prepared actions
   below.
3. Click the `Compare` button for one of the actions in the upper right corner.
4. Click the `Start comparing` button for the other action.
5. The difference between the actions are highlighted.

Prepared actions:
https://buildbar.meroton.com/browser/buildbarn-meetup-2026/blobs/sha256/action/35f81177739aaee2b6275a88696a7e40408c71a4505758567c2ce5296d7c4dcd-224
https://buildbar.meroton.com/browser/buildbarn-meetup-2026/blobs/sha256/action/9cccdc569ee6426dd08acaffd91a55607297d617a362bca1c3a48c37d7f1f842-224

### View test action output

BB-portal lets you view and download the output of test actions.

1. Run `bazel test @abseil-hello//...`
2. Open the invocation in bb-portal by clicking the link in the invocation log.
3. Click on the test tab for the invocation, and click on the test in the list.
4. There the test log and test.xml can be viewed and downloaded.
