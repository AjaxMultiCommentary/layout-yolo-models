`layout-yolo-models` contains two [YOLOv5m](https://pytorch.org/hub/ultralytics_yolov5/#:~:text=YOLOv5%20%F0%9F%9A%80%20is%20a%20family,to%20ONNX%2C%20CoreML%20and%20TFLite) checkpoints trained for page layout analysis on classical commentaries. Detailed information can be found in [this paper](PAPER_LINK). 


# Labels

Labelling regions follows the [Segmonto](https://segmonto.github.io/)-compatible annotations proposed in [the paper](PAPER_LINK):

| Region                 | Coarse           | Fine                             |
| ---------------------- | ---------------- | -------------------------------- |
| commentary             | MainZone         | MainZone:commentary              |
| critical apparatus     | MarginTextZone   | MarginTextZone:criticalApparatus |
| footnotes              | MarginTextZone   | MarginTextZone:footnotes         |
| page number            | NumberingZone    | NumberingZone:pageNumber         |
| text number            | NumberingZone    | NumberingZone:textNumber         |
| bibliography           | MainZone         | MainZone:bibliography            |
| handwritten marginalia | MarginTextZone   | MarginTextZone:handwrittenNote   |
| index                  | MainZone         | MainZone:index                   |
| others                 | CustomZone       | CustomZone                       |
| printed marginalia     | MarginTextZone   | MarginTextZone:printedNote       |
| table of contents      | MainZone         | MainZone:ToC                     |
| title                  | TitlePageZone    | TitlePageZone                    |
| translation            | MainZone         | MainZone:translation             |
| appendix               | MainZone         | MainZone:appendix                |
| introduction           | MainZone         | MainZone:introduction            |
| preface                | paratext         | MainZone:preface                 |
| primary text           | MainZone         | MainZone:primaryText             |
| running header         | RunningTitleZone | RunningTitleZone                 |

Each model is trained with its respective label set (`coarse` or `fine`). 


# Data

Models are trained with the datasets used in the paper, including commentaries under copyright commentaries. Public domain data has been released and can be found [here](https://github.com/AjaxMultiCommentary/GT-commentaries-layout). 

# Training parameters

| name            | value                     |
| --------------- | ------------------------- |
| Epochs          | 200                       |
| Hyperparameters | YOLOv5 defaults           |
| Image size      | 1280                      |
| YOLO version    | YOLOv5, v6.1-356-g4d8d84b |
| Model size      | YOLOv5m                   |


# Results


# Caveats

⚠️ These models are beta-tryouts. They are mainly released because part of the training data is still under copyright and cannot be released. **This does by no means imply that our models are ready for use in production**. As shown in the results section, some regions remain poorly recognized. 

⚠️ Our [experiments](PAPER_LINK) also show that our models perform poorly on unseen layout types and editions. Evaluating a model on a set of completely unseen commentaries causes a performance drop of about 30% with respect to the in-domain test-set. The same drop is to be expected with your data. We therefore would recommend continuing training on a few in-domain instances to mitigate this. 
