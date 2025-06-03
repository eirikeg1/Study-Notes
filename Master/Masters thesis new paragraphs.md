# From Pixels to Play: Automating Dribble and Tackle Detection in Football
## Leveraging a Finite State Machine and Machine Learning for Event Detection

# Chapter 1
## Research methods

## Main contributions
\section{Main Contributions}\label{sec:main_contributions_intro}
This master's thesis makes the following primary contributions to the field of sports video analysis, specifically focusing on the automated detection of dribble and tackle events in football:

\begin{enumerate}
\item \textbf{Development of a Comprehensive Positional Data Extraction Pipeline:} We introduce and evaluate an end-to-end pipeline designed to automatically process raw football broadcast videos and extract essential player and ball positional data. This pipeline integrates various computer vision techniques, including automated video clipping, scene filtering, object detection using fine-tuned YOLO models, player tracking, and an investigation into 2D top-down pitch coordinate estimation and team identification. A key aspect is the use of annotation interpolation to enhance data consistency and reduce computational load, making the extraction of data suitable for subsequent event detection feasible.

\item \textbf{Design and Implementation of a Novel Rule-Based Event Detection Algorithm:} We propose, develop, and prototype a novel Finite State Machine (FSM) based algorithm for the specific detection of successful dribbles and tackles. This knowledge-driven approach explicitly models the definitions provided by domain experts (Opta Sports) and the observable sequential dynamics of these player interactions. This method offers an interpretable alternative to purely data-driven techniques, particularly advantageous given the current scarcity of large-scale, publicly annotated datasets for these fine-grained events.

\item \textbf{Investigation into Semi-Automated Dataset Creation:} A significant contribution is the systematic investigation into the viability of using the complete proposed pipeline (from raw video input, through positional data extraction, to FSM-based event detection) for the semi-automated creation of an initial, manually verified dataset of dribble and tackle events. This work explores a practical pathway to address the critical data bottleneck that currently hinders the development of supervised machine learning models for these specific actions, by facilitating a more efficient data curation process.

\item \textbf{Public Release of Research Artefacts:} To promote transparency, reproducibility, and further research in this area, all code developed for the data extraction pipeline and the FSM-based event detection algorithm will be made publicly available. This includes links to the video data used for evaluation where copyright permits.

\end{enumerate}


# Bibtex citation
## Thesis
```latex
@thesis{eggset_2025_dribble_and_tackle_detection,
  author = {Eggset, Eirik},
  type = {Master's thesis},
  title = {From Pixels to Play: Automating Dribble and Tackle Detection in Football},
  year = {2025},
  institution= {University of Oslo},
  % howpublished = {\url{}},
  note = {Unpublished master's thesis, accessed 2025-05-14}
}
```

## Github
```latex
@misc{eggset_2025_dribble_detection_code,
  author       = {Eggset, Eirik},
  title        = {Dribbling Detection Pipeline},
  year         = {2025},
  howpublished = {\url{https://github.com/eirikeg1/dribbling-detection-pipeline}},
  note         = {Accessed: 2025-05-14}
}
```

