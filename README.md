# YOLOv5m models for Historical Commentaries

`layout-yolo-models` contains two [YOLOv5m](https://pytorch.org/hub/ultralytics_yolov5/#:~:text=YOLOv5%20%F0%9F%9A%80%20is%20a%20family,to%20ONNX%2C%20CoreML%20and%20TFLite) checkpoints trained for page layout analysis on classical commentaries. Detailed information can be found in [this paper](PAPER_LINK). 

## Demo

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/mromanello/d59b9d5f5c25f36ee088ca7b566fee25/HEAD?labpath=demo.ipynb) 

[This notebook](https://mybinder.org/v2/gh/mromanello/d59b9d5f5c25f36ee088ca7b566fee25/HEAD?labpath=demo.ipynb) offers a quick demo of how the models can be used to segment other commentaries available on the Internet Archive. 

## Data

Models are trained with the datasets used in the paper, including under copyright commentaries. Public domain data has been released as the [GT4HistCommentLayout](https://github.com/AjaxMultiCommentary/GT-commentaries-layout) dataset. Please refer to [`stats.txt`](./stats.txt) for detailed statistics about the data. 

## Labels
<details>
<summary>More</summary>

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
</details>


## Training parameters

<details>
<summary>More</summary>

| name            | value                     |
| --------------- | ------------------------- |
| Epochs          | 200                       |
| Hyperparameters | YOLOv5 defaults           |
| Image size      | 1280                      |
| YOLO version    | YOLOv5, v6.1-356-g4d8d84b |
| Model size      | YOLOv5m                   |

</details>

## Results

<details>
<summary>More</summary>

Results are computed on the test set (see paper) using [mean-average-precision](https://github.com/bes-dev/mean_average_precision), which yields results inferior to YOLOv5's native evaluation tool. 

### Coarse model

| mAP   | MainZone | MarginTextZone | NumberingZone | RunningTitleZone | TitlePageZone |
|-------|----------|----------------|---------------|------------------|---------------|
| 0.662 | 0.862    | 0.750          | 0.892         | 0.950            | 0.133         |

### Fine model

| mAP         | CustomZone:other | MainZone:ToC | MainZone:appendix | MainZone:bibliography | MainZone:commentary | MainZone:introduction | MainZone:preface | MainZone:primaryText | MainZone:translation | MarginTextZone:criticalApparatus | MarginTextZone:footnote | MarginTextZone:printedNote | NumberingZone:pageNumber | NumberingZone:textNumber | RunningTitleZone | TitlePageZone |
|-------------|------------------|--------------|-------------------|-----------------------|---------------------|-----------------------|------------------|----------------------|----------------------|----------------------------------|-------------------------|----------------------------|--------------------------|--------------------------|------------------|---------------|
| 0.690006852 | 0.483957231      | 0            | 0.83333331        | 0.75                  | 0.93403023          | 0.78166848            | 0.69999999       | 0.64651763           | 0.85653406           | 0.8403641                        | 0.71988797              | 0.66250002                 | 0.96583301               | 0.88592309               | 0.93956083       | 0.04          |


### Examples

Here's a quick example of a good prediction... 

![Good Prediction](./examples/cu31924087948174_0087.png)

...and of a bad prediction (in this case, two regions overlapping).

![Bad Prediction](./examples/cu31924087948174_0011.png)

</details>

## Caveats

⚠️ These models are beta-tryouts. They are mainly released because part of the training data is still under copyright and cannot be released. **This does by no means imply that our models are ready for use in production**. As shown in the results section, some regions remain poorly recognized. 

⚠️ Our [experiments](PAPER_LINK) also show that our models perform poorly on unseen layout types and editions. Evaluating a model on a set of completely unseen commentaries causes a performance drop of about 30% with respect to the in-domain test-set. The same drop is to be expected with your data. We therefore would recommend continuing training on a few in-domain instances to mitigate this. 

## Citation

If you use this dataset in your research, please cite the following publication:

```
@inproceedings{najem-meyer_page-layout-analysis_2022,
  title = {Page {{Layout Analysis}} of {{Text-heavy Historical Documents}}: A {{Comparison}} of {{Textual}} and {{Visual Approaches}}},
  booktitle = {Proceedings of the {{Conference}} on {{Computational Humanities Research}} 2022},
  author = {{Najem-Meyer}, Sven and Romanello, Matteo},
  year = {2022},
  pages = {36--54},
  publisher = {{CEUR-WS}},
  address = {{Antwerp}},
  url = {https://ceur-ws.org/Vol-3290/long_paper8670.pdf}
}
```

## Acknowledgements

Models in this repository were produced in the context of the Ajax Multi-Commentary project, funded by the Swiss National Science Foundation under an Ambizione grant [PZ00P1\_186033](http://p3.snf.ch/project-186033).

