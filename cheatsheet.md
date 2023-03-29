---
layout: page
title: Cheetsheet
---


* this unordered seed list will be replaced by the toc
{:toc}

## Probability Logic Table

| **Voting** |                                                                                   **Formula**                                                                                  |        **Comment**        |
|:----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------:|
|    1oo1    |                                                                                  P<sub>A</sub>                                                                                 |   Single element system   |
|    1oo2    |                                                                           P<sub>A</sub>P<sub>B</sub>                                                                           |       Both devices fail  |
|    2oo2    |                                                           P<sub>A</sub> + P<sub>B</sub> – P<sub>A</sub>P<sub>B</sub>                                                           |   Either device fails   |
|    1oo3    |                                                                     P<sub>A</sub>P<sub>B</sub>P<sub>C</sub>                                                                    |   All devices must fail   |
|    2oo3    |                         P<sub>A</sub>P<sub>B</sub> + P<sub>A</sub>P<sub>C</sub> + P<sub>B</sub>P<sub>C</sub> – 2P<sub>A</sub>P<sub>B</sub>P<sub>C</sub>                        | Any two devices must fail |
|    3oo3    | P<sub>A</sub> + P<sub>B</sub> + P<sub>C</sub> – P<sub>A</sub>P<sub>B</sub> – P<sub>A</sub>P<sub>C</sub> – P<sub>B</sub>P<sub>C</sub> + P<sub>A</sub>P<sub>B</sub>P<sub>C</sub> |      Any device fails     |


## PFD Equations
PFD equations (not simplified) assuming all devices in the voting scheme have the same lambda:

| **Voting** |                                                                                     **PFD**                                                                                    |                      **PFD Avg**                     |
|:----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------:|
|    1oo1    |                                                                          $$1 - e^{-\lambda t}$$                                                                          | $$1 + \frac{e^{-\lambda T}-1}{\lambda T}$$ |
|    1oo2    |                                                                           $$1 - 2e^{-\lambda t} + e^{-2\lambda t}$$            | $$1 + \frac{2e^{-\lambda T}-2}{\lambda T} + \frac{1-e^{-2\lambda T}}{2\lambda T}$$                  |
|    2oo2    |                                                         $$ 1 - e^{-2\lambda t} $$                                                         |   $$1 + \frac{e^{-2\lambda T}-1}{2\lambda T}$$                |
|    1oo3    | $$1 - 3 e^{- \lambda t} + 3 e^{- 2 \lambda t} - e^{- 3 \lambda t}$$ | $$1 - \frac{11}{6 \lambda T} + \frac{3 e^{- \lambda T}}{\lambda T} - \frac{3 e^{- 2 \lambda T}}{2 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}$$        |
|    2oo3    | $$1 - 3 e^{- 2 \lambda t} + 2 e^{- 3 \lambda t}$$   | $$1 - \frac{5}{6 \lambda T} + \frac{3 e^{- 2 \lambda T}}{2 \lambda T} - \frac{2 e^{- 3 \lambda T}}{3 \lambda T}$$ |
|    3oo3    | $$1 - e^{- 3 \lambda t}$$|    $$1 - \frac{1}{3 \lambda T} + \frac{e^{- 3 \lambda T}}{3 \lambda T}$$               |
