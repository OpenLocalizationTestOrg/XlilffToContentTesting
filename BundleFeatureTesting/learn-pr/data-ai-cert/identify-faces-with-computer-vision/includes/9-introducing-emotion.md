---
ms.openlocfilehash: 6a6eba0065b92c416c29b33138bed28174a63538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
While working with your Face API service, you might notice that it can return general emotion values through the **Detect method emotion** attribute. You probably also notice that the returned information is sparse and typically only registers a level of happiness. 

The Cognitive Services Emotion API builds on these results by using additional methods and algorithms to detect a rich set of emotions in images of human faces.

![Two people's faces express emotion](../media/8-introducing-emotion-concepts.png)

The Emotion API provides advanced face analysis algorithms to assign a confidence level for the following emotions: anger, contempt, disgust, fear, happiness, neutral (the absence of emotion), sadness, and surprise.

## <a name="scores-and-locations"></a>Scores and locations

As in the Face API, the Emotion API associates detected faces with face *locations*. But the Emotion API adds a collection of values to the payload describing the likelihood of various emotions. The analysis is based on a variation of confidence levels, referred to as *scores*.

- **Score**: The likelihood or level of confidence that a face displays a specific emotion
- **Location**: The top, left, height, and width of a region in the image that displays a face

![A group of faces are analyzed by the Emotion API. JSON code shows the scores and locations of the faces](../media/8-introducing-emotion-score-location.png)

Scores, just like confidence levels, are similar to percentages. Their range is 0.0 to 1.0. The higher the value, the more certain the service is that the emotion is accurate.
