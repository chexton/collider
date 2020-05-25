#Collider

Collider is a "message bus" designed to ensure customers receive the highest quality, most relevant message. 

Designed for engineers to manage messages sent across all aspects of the customer lifecycle, Collider filters all marketing, product engagement and transactional messages to ensure a consistent and high quality customer experience.

Our goal is to:

- Increase the quality of the messages your customers receive.
- Ensure messages your customers receive are tightly integrated with your core digital product and service offerings.
- Increase the reliability and accuracy of the messages your customers receive.
- Make this achievable at any scale.

## What Collider does

In order to ensure the best / "right" message reaches a customer, most messaging platforms attempt to move the creation and deployment of every message to a central, monolothic, UI-based platform (e.g. Salesforce Marketing Cloud).

Collider is built on the idea that marketing, product engagement and transactional emails can and should be triggered from alternate systems and that the determination of __which__ message to send should be decoupled from the content creation and triggered timing of that message. Under this model, content creation and message triggering are moved "upstream" and left to the best team for each job (marketing, product and engineering). Rather than each upstream system triggering messages directly to customers, messages are instead sent to Collider, which maintains a "queue" for each individual recipient. Collider then applies global rules to that queue, ensuring messages are "released" in line with the rules. In other words, rather than messages being sent first-in-first-out (FIFO) whenever they're triggered, Collider temporarily places every message in a queue, inspects it and applies rules you've configured and determines which messages in the queue should go out first.

Collider is software with a CLI-based interface that enables you to:

- Set global rules for message delivery, such as:
-- Users should only receive one marketing message every two days.
-- Marketing messages tagged with A, B or C should only survive in the queue for up to four days.
-- Transactional emails should always be released immediately.
-- Users should never receive a message with the same subject twice.
-- Users should receive messages on the channel they last engaged with first, i.e. prioritise push over email messages.
-- Product engagement messages should be released between 8-10am in the recipient user's timezone only.
- Tag messages from incoming systems for grouping and filtering.
- Log all decisions via a log drain for future analysis.

## What Collider does not do

- Provide any interface for building or managing email content.
- Provide any interface for triggering messages.

## How Collider works

A Collider project is a collection of `.yml` and `.sql` files. At a minimum, the directory must contain:

- **Rules:** A rule is a single `.yml` file that contains a set of conditions and the types of messages to apply those to (based on message source, content, tags, etc.).
- **Hierarchy:** A hierarchy is a single `.yml` file that describes the order in which rules should be applied. Different hierarchies can be applied to separate incoming message streams.

Collider will observe all incoming messages and match against the defined rules and hierarchy in realtime. All decisions will be logged, and messages that are not released immediately will be "held" in the queue for an individual customer until released or discarded. Collider also providers a means to query the remaining messages in a queue for a given customer.