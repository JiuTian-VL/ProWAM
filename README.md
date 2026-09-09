<div align="center">

<h2 class="papername">
Learning to Use Imagination:<br>
Progress-Conditioned Future Utilization for World Action Models
</h2>

<div>
    <a href="https://scholar.google.com.hk/citations?user=0GtAUPoAAAAJ&hl=zh-CN&oi=sra" target="_blank">Yijie Zhu</a><sup>1,2</sup>,
    <a href="https://zitongyu.github.io/" target="_blank">Zitong Yu*</a><sup>2</sup>,
    <a href="https://liwei-2013.github.io/" target="_blank">Wei Li</a><sup>1</sup>,
    <a href="https://openreview.net/profile?id=~Hui_Ma7" target="_blank">Hui Ma</a><sup>2</sup>,
    <a href="https://wenli-vision.github.io/" target="_blank">Wen Li</a><sup>3</sup>,
    <a href="https://rshaojimmy.github.io/OrionLab/" target="_blank">Rui Shao*</a><sup>1</sup>,
    <a href="https://liqiangnie.github.io/" target="_blank">Liqiang Nie</a><sup>1</sup>
</div>

<br>

<sup>1</sup>School of Computer Science and Technology, Harbin Institute of Technology, Shenzhen<br>
<sup>2</sup>Great Bay University<br>
<sup>3</sup>University of Electronic Science and Technology of China<br>

*Corresponding authors<br>

<a href="https://arxiv.org/abs/2609.06578">
  <img src="https://img.shields.io/badge/arXiv-2609.06578-b31b1b.svg?logo=arxiv" alt="arXiv">
</a>


<h3 align="center">
    <strong>
    🛠️ We're still cooking — Stay tuned! 🛠️<br>
    ⭐ Give us a star if you like it! ⭐<br>
    ✨ If you find this work useful for your research, please kindly cite our paper. ✨
    </strong>
</h3>

</div>

## :fire: Introduction

**ProWAM** is a **Progress-Conditioned World Action Model** that learns how to
adaptively use imagined future information for robotic manipulation. Existing
World Action Models (WAMs) incorporate future visual dynamics into action
generation, but they often use imagined futures through fixed or progress-agnostic
interaction patterns. This can introduce distracting or unreliable predictive
cues when the utility of future information changes during task execution.

The key insight of **ProWAM** is that imagined futures should not be used
uniformly throughout manipulation. Instead, their influence should depend on the
robot's **execution progress**. Future-oriented cues can be particularly useful
during search, transit, and approach stages, while contact-rich stages such as
grasping, handover, and placement require stronger grounding in immediate
interaction feedback. Moreover, even within the same progress state, different
future latents may have different relevance to the current control objective.

To address this problem, **ProWAM** introduces execution progress as an explicit
intermediate representation for adaptive future utilization. It consists of two
tightly coupled components:

- **Self-Supervised Dual-Temporal Progress Encoder (SS-DTPE)** learns structured
  progress representations by integrating short-term action-observation feedback
  with long-term recurrent execution history, without requiring manual progress
  annotations.
- **Hierarchical Progress-Conditioned Imagination Modulation (HPIM)** adapts the
  use of imagined futures according to execution progress through inter-progress
  global modulation and intra-progress future-latent relevance.

Together, these components enable **stage-adaptive** and **latent-specific**
imagination utilization, allowing the action stream to exploit imagined futures
more effectively across different execution stages and future latents.

We also provide a comprehensive comparison between vanilla VLAs, standard WAMs,
and our progress-conditioned ProWAM framework.

<div align="center">
<img src="asserts/intro.png" width="85%">
</div>

## :gear: Method

The overall framework of **ProWAM** is illustrated below. Given a visual
observation, a task instruction, and the previously executed action, ProWAM
first estimates the current execution progress using **SS-DTPE**. The learned
progress representation captures both recent action-observation feedback and
accumulated task history.

Conditioned on this progress representation, **HPIM** adaptively regulates how
imagined future latents are used during action generation. At the inter-progress
level, it adjusts the overall reliance on future information across execution
stages. At the intra-progress level, it differentiates individual future latents
within the same progress state. The resulting progress-conditioned modulation
enables the WAM backbone to selectively strengthen useful future cues while
suppressing distracting or unreliable ones.

<div align="center">
<img src="asserts/prowamv3.png" width="100%">
</div>

## :bar_chart: Results

**ProWAM** is evaluated on five simulation benchmarks and two real-world robotic
platforms, covering general manipulation, robustness and generalization,
progress-aware execution, temporal memory, and long-horizon real-world
manipulation.

Across simulation and real-world settings, ProWAM consistently improves over
strong VLA and WAM baselines. The gains are especially clear on progress-aware
and long-horizon tasks, where the robot must maintain coherent task advancement
and adapt its use of imagined futures across different execution stages.




## :movie_camera: Videos







<table>
  <tr>
 <td align="center" width="33%">
  <video src="https://github.com/user-attachments/assets/ff2b09f5-aeca-484b-b742-4fa2bf73e18d" controls muted width="100%"></video>
  <br>
  <b>Transfer Objects from Tray to Tray</b>
</td>
    <td align="center" width="33%">
      <video src="https://github.com/user-attachments/assets/ccc69a42-7e9d-450f-948c-1bbb92f9d434" controls muted width="100%"></video>
      <br>
      <b>Stack Three Blocks</b>
    </td>
    <td align="center" width="33%">
      <video src="https://github.com/user-attachments/assets/18b5c886-a2e3-4cce-ac02-39872316039f" controls muted width="100%"></video>
      <br>
      <b>Stack Bowl on Plate</b>
    </td>
  </tr>
  <tr>
    <td align="center" width="33%">
      <video src="https://github.com/user-attachments/assets/4673696c-7808-4ca6-a6bd-cca30bd84417" controls muted width="100%"></video>
      <br>
      <b>Clear Objects into Bin</b>
    </td>
    <td align="center" width="33%">
      <video src="https://github.com/user-attachments/assets/5c6ed73d-6c83-4d9e-ac1e-1903716b51d9" controls muted width="100%"></video>
      <br>
      <b>Fold Cloth</b>
    </td>
    <td align="center" width="33%">
      <video src="https://github.com/user-attachments/assets/afffb4df-10bb-4614-a405-36bcb15e7290" controls muted width="100%"></video>
      <br>
      <b>Drawer Manipulation</b>
    </td>
  </tr>
</table>








## :open_file_folder: Code Release

We are preparing the code, pretrained checkpoints, and evaluation scripts.
Please stay tuned.

- [ ] Training code
- [ ] Evaluation code
- [ ] Pretrained checkpoints
- [ ] Real-world rollout videos
- [ ] Simulation benchmark scripts

## :memo: Citation

If you find this work useful for your research, please kindly cite our paper:

```bibtex
@article{zhu2026prowam,
  title={Learning to Use Imagination: Progress-Conditioned Future Utilization for World Action Models},
  author={Zhu, Yijie and Yu, Zitong and Li, Wei and Ma, Hui and Li, Wen and Shao, Rui and Nie, Liqiang},
  journal={arXiv preprint arXiv:2609.06578},
  year={2026}
}
