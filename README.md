# Test-Time Ground-Truth Dependency in Reprojection-Based Multi-Hypothesis 3D Human Pose Estimation: Measurement and a Corrected Configuration

> **Status:** the paper is under peer review. The code and result files will be published in this
> repository after the paper is accepted. Until then, the repository contains only this page.

## About the paper

Generative lifters for monocular 3D human pose estimation, such as D3DP and FMPose3D, draw many
candidate poses (hypotheses) for each input and combine them according to how well each one
reprojects onto the observed 2D keypoints. Reprojection needs the position of the pose in camera
space, which these models do not predict. In the released evaluation code of both methods, this
position (the root translation) comes from the 3D ground truth of each test sample.
The reported metric is still computed correctly; the question is how much of the benefit of the
aggregation step remains when the ground truth is not available, as in deployment.

The paper replaces the ground-truth root translation with a least-squares estimate solved from the
2D keypoints, changes nothing else, and measures the effect on the full Human3.6M test set with the
authors' released checkpoints. It then bounds what several test-time strategies can recover without
the ground truth, and reports a configuration of the released FMPose3D model that is more accurate
for detector-based 2D input while using fewer network evaluations. With ground-truth 2D input, that
configuration is not better, and the paper states this condition with the result.

## What will be released

- The root-substitution hook for the D3DP evaluation loop. It is switched by an environment
  variable, and its default setting leaves the original code path unchanged.
- The closed-form least-squares solver for the root translation.
- The evaluation scripts for the experiments reported in the paper.
- The logged result files behind every table and figure, with a script that recomputes each number
  in the paper from those files.
- The scripts that draw the figures from the result files.

The Human3.6M and MPI-INF-3DHP datasets are not redistributed; they are available from their
providers under their own terms. All experiments use the checkpoints released by the D3DP and
FMPose3D authors, and no new data were collected.

## Built on

| Project | Repository | Commit used | License |
|---|---|---|---|
| D3DP (Shan et al., ICCV 2023) | [paTRICK-swk/D3DP](https://github.com/paTRICK-swk/D3DP) | `afcdd05` | MIT |
| FMPose3D (Wang et al., CVPR 2026) | [AdaptiveMotorControlLab/FMPose3D](https://github.com/AdaptiveMotorControlLab/FMPose3D) | `54dd3fb2` | Apache 2.0 |

We thank the authors of both projects for releasing their code and trained models.

## Citation

A citation entry will be added here when the paper is published.

## Contact

Trinh Quoc Nguyen (corresponding author), trinhnq.3@dhv.edu.vn

Editors and reviewers who need the code during the review can request access from the
corresponding author.

## License

The license will be set at release. Code derived from D3DP and FMPose3D will keep the terms of the
MIT and Apache 2.0 licenses, respectively.
