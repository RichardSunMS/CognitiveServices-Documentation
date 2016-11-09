<!-- 
NavPath: Content Moderator
LinkLabel: Overview
Url: Content-Moderator/documentation
Weight: 200
-->

# Overview #
Content moderation is the process of monitoring User Generated Content (UGC) on online and social media web sites, chat and messaging platforms, and peer communication platforms to track, flag, assess and filter out offensive and unwanted content that creates risks for businesses. The content can include text, images, and videos.

## Where would you use it ##
Content moderation for all three types of content has several benefits.They are

- Image moderation works great for profile pictures, social media, business documents, and image sharing sites.
- Text moderation benefits communities, family-based web sites, in-game communities, chat and messaging platforms, and user-generated content marketing.
- Video moderation is used for video publishing sites, news sites, and video content sites, to take a few examples.

## Three ways to moderate content ##
- Automated moderation applies machine learning and AI to cost-effectively moderate at scale
- Human moderation uses teams and the community to moderate all content.
- Hybrid moderation combines automated moderation augmented by the human-in-the-loop (human oversight).

Microsoft Content Moderator enables all three scenarios.

## Automated moderation APIs ##
You can subscribe to the Moderator APIs for text, images and videos to automatically moderate large amount of content cost-effectively, at scale with only a few lines of code.

## The human review tool ##
The review tool enables the human-in-the-loop capability with it’s support for human review teams. You can invite other users, track pending invites, and assign permissions to your team members. It will internally call the automated moderation APIs and make the reviews available right within your web browser. The review tool currently supports image reviews, but text and videos are on the roadmap.

## Combining the APIs with the review tool ##
Combine the image moderation APIs with the human review tool to quickly implement an end-to-end hybrid moderation solution for images. Use the review tool’s API to auto-moderate images in bulk and review the tagged images within the review tool. Provide your API callback point so that you get notified when the reviewers submit their decisions. This allows you to automate the post-review workflow by integrating with your own systems.
