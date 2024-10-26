# How Scene Graphs Transform Images into Rich Visual Narratives
To truly understand an image, inferring the relationships between the objects within the image is crucial for effectively telling a "visual story." Scene graphs allow us to map out how objects within an image interact with one another. In this article, I will walk you through on how to build a visual story of the image given below using YOLOv5 for object detection and NetworkX for relationship extraction, visualizing these interactions to create a meaningful image representation. We will also use an LLM to describe the Graph’s output.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1xvCS2vkTCy8WOJ2fj1_UMUeZ8xAo7Lt6?usp=sharing)
*The code for building and analyzing the scene graph using YOLOv5 and NetworkX is available in the Colab notebook linked above.*


![image](https://github.com/user-attachments/assets/f1a3c5c0-36f1-4ce9-88d7-76addd7ff0a5)

In rthe above image, we see two young boys engaged in a tennis match on a court. The scene captures a dynamic moment where both players are actively involved in the game. The boy on the left, dressed in blue, is positioned near the net with his racket raised (much like Roger Federer during his peak), indicating he is likely preparing to hit the ball. His posture suggests he is about to swing, adding a sense of motion to the image. On the right, the second boy, dressed in red, appears to be in a defensive position, preparing to receive the ball, which is visible in the air above his head.

The setting includes a tennis court with a net in the center, separating the two players, and a wooden fence in the background, with trees on either side. The image captures the energy of the game, with the players seemingly mid-action, suggesting a fast-paced exchange. Now, if we need to build a relationship model which provides an explainable AI scene for this match, we need to captures the positions and interactions of the players and the ball.

In this case, we combine object detection with relationship extraction to produce a comprehensive scene graph of a tennis match between two players. This can be done via Yolo5 which captures the bounding boxes of the objects and NetworkX to capture the relationships. After that, we can hook-up the entire scene with an LLM to get the Explainability.

## Object Detection Using YOLOv5
We begin by detecting the main objects within the tennis match image using the pre-trained YOLOv5 model. YOLOv5's architecture allows for the real-time identification of objects such as people, tennis rackets, and the ball. The results are shown in the form of bounding boxes that localize each object in the image. This process involves passing the image through the YOLOv5 model, which outputs the detected objects and their respective bounding box coordinates.

![image](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2b89cf65-24f2-483c-8c53-636b9fa9d871_737x555.png)

The primary objects detected in this image are:

- **Person 1**: The player on the left side of the court.
- **Person 2**: The player on the right side.
- **Tennis racket**: Held by both players.
- **Sports ball**: Positioned near the center of the court.
- Tennis court and net.

## Relationship Extraction and Visualization
We employed NetworkX to visualize the scene graph, representing each object and its relationships. The graph not only shows which objects are interacting but also the nature of these interactions.

![image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F51695a15-1752-4e92-8d89-33f07e9cb3a0_3060x3060.png)

The scene graph provides a structured, visual interpretation of the tennis match.

- **Person 1** and **Person 2** are connected by the relationship **"aiming towards"**, indicating that **Person 1** is preparing to hit the ball towards **Person 2**.
- The ball is connected to **Person 1** by the relationship **"about to hit"**.
- The ball is also connected to the net with the relationship **"above"**, demonstrating the ball’s current position in the game.

In this visualization, nodes representing people are shown in orange, objects such as the racket and ball in gray, and the environment (i.e., tennis court and net) in green. Edges between these nodes represent the interactions, and each relationship is labeled with its respective weight, indicating the strength or significance of the interaction.

**Applications of Scene Graphs**

The application of scene graphs extends beyond sports imagery. In fields such as robotics and autonomous vehicles, understanding the relationships between objects is crucial for decision-making. Scene graphs can also enhance image retrieval systems by allowing searches not just for objects, but for specific interactions between those objects (e.g., "a person hitting a ball").

Additionally, scene graphs offer benefits in understanding complex environments. For instance, in the context of smart cities, scene graphs could help manage traffic by modeling how vehicles interact with traffic signals, pedestrians, and each other.

**The combination of object detection and relationship extraction via Scene Graphs has a wide range of applications:**

- **Robotics:** Scene graphs can help robots understand their environment, making decisions based on object-object interactions. For example, a robot could navigate a room by recognizing that a chair is in front of a table.

- **Autonomous Vehicles:** In autonomous driving, scene graphs can help vehicles understand traffic scenarios by recognizing not just objects (like other cars or pedestrians) but also their spatial and behavioral relationships (e.g., car A is turning left, pedestrian is crossing the street).

- **Image Retrieval:** Imagine searching for images based on relationships, not just objects. Instead of simply searching for "tennis", you could search for "person hitting ball on tennis court" — a much more specific and accurate search query powered by scene graphs.

**Now Hookup Everything with an LLM to Generate a Story**
## Here is a Quick Recap

```mermaid
flowchart TD
    A[Input Image] --> B[Run YOLOv5]
    B --> C[Detect Objects Bounding Boxes]
    C --> D{Extract Relationships NetworkX}
    D --> E[Create Scene Graph]
    E --> F[Visualize Interactions]
    F --> G[Integrate with GPT-4 LLM]
    G --> H[Generate Story]
