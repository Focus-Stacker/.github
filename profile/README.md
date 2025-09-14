# 🔬 Focus Stacker for Mac — Precision Focus Stacking for Macro, Product & Landscape

![Focus Stacker Icon](https://is1-ssl.mzstatic.com/image/thumb/Purple124/v4/7f/8b/a4/7f8ba4fd-f8be-d2d8-3430-8ea8a74b6391/pr_source.png/643x0w.jpg)

<div align="center" style="margin:14px 0 16px;">
  <a href="https://focus-stacker.github.io/.github">
    <img src="https://img.shields.io/badge/⬇️_GET_FOCUS_STACKER_FOR_MAC-darkslateblue?style=for-the-badge&logo=camera&logoColor=white" alt="Get Focus Stacker for Mac">
  </a>
</div>

---

## ❓ What is Focus Stacker?

**Focus Stacker** is a macOS application that combines a series of photographs taken at **incremental focus distances** into a single image with **maximum depth of field** and **razor-sharp detail**. Where a single exposure may only render a sliver of a subject in focus—think macro florals, jewelry, insects, watch movements, circuit boards, or product shots—Focus Stacker algorithmically selects the sharpest pixels from each frame and blends them into a seamless composite. The result is an image that preserves **micro-detail from front to back** while avoiding the diffraction and noise penalties you’d get from stopping way down or pushing ISO.

Under the hood, the app performs **contrast-based focus metrics** on overlapping tiles across the stack, building a confidence map that indicates which source frame contributes the sharpest information in each region. It then generates a **depth map** and uses multi-band blending to avoid halos at edges where planes of focus intersect. Because texture varies across materials—matte petals, glossy metals, hairs, textured paper—the app adapts window sizes and frequency bands to retain fine threads without ringing while keeping smooth gradients free of stitching artifacts.

Focus Stacker is designed for **real-world workflows**, not just lab scenes. It tolerates small changes in magnification from focus breathing, corrects subtle perspective shifts, and can automatically align handheld sequences with sub-pixel registration. For tripod-based and rail-driven stacks, you can enable strict alignment and lens-profile-aware scaling for the cleanest possible composite. The preview renders quickly on Apple Silicon so you can evaluate the depth map, refine parameters, and iterate without waiting for a full export.

Beyond macro, the app excels at **tabletop product photography** (packaging, cosmetics, watches, tech), **food** with layered garnishes, **archival digitization** of relief objects, and **landscape focus stacks** where foreground rocks and distant peaks must both be crisp. It also pairs well with **focus bracketing** modes found in many cameras; just drop the burst into Focus Stacker, choose a preset (Macro, Product, Landscape, or Scientific), inspect the depth mask, and export to 16-bit TIFF, PNG, or layered PSD for retouching.

Focus Stacker respects your files and time. It reads **RAW-derived TIFF/PNG/JPEG** exports or camera JPEGs, preserves **EXIF/XMP** metadata, supports **color-managed workflows** (sRGB/Adobe RGB/ProPhoto), and writes **non-destructive** side data during the session. Batch mode processes entire jobs unattended, with per-set naming tokens and export recipes (e.g., a 16-bit master plus a web JPEG). From stack capture to publish-ready output, it minimizes friction so you can focus on lighting, styling, and client deadlines rather than pixel surgery.

---

## ℹ️ About Focus Stacker (Deep Dive)

Focus Stacker grew out of the practical challenges photographers face when pushing depth of field beyond optical limits. Stopping down past f/11–f/16 invites **diffraction softening**; turning up ISO lifts shadow noise; focus rails and macro bellows introduce **focus breathing** and tiny perspective drifts; reflective surfaces create halos where sharp/soft meet. The app addresses each pain point with a pipeline tuned for **fidelity** and **forgiveness**:

- **Robust Alignment:** Sub-pixel translation, rotation, and scale compensation handle breathing and tiny tripod shifts. For extreme magnifications, a **non-linear warp refinement** reduces parallax on near-field details without bending geometry in the far plane.  
- **Adaptive Sharpness Metrics:** Multiple measures (Laplacian variance, gradient energy, and band-limited contrast) are fused to estimate per-pixel focus confidence. Fine textures benefit from small windows; smooth zones use larger windows to avoid noise selection.  
- **Depth Map Smoothing with Edge Respect:** A guided filter regularizes the depth map, preserving edges from hairs, filigree, and PCB traces while avoiding stair-stepping. This reduces zipper artifacts when the blend transitions across edges.  
- **Multi-Band Compositing:** The final composite uses frequency-split blending to prevent halos, keeping high-frequency detail crisp while merging low-frequency tones naturally. Materials like brushed metal or satin fabrics retain their character without ringing.  
- **De-Halo & Fringe Controls:** Chromatic fringes and bright-edge halos often appear at depth boundaries. A local de-halo pass attenuates overshoot; optional **CA guard** limits color edge contamination pulled from neighboring frames.  
- **Motion & Ghost Handling:** If a leaf, flame, or micro-subject moves between frames, a **ghost detection** pass flags conflicting regions. You can prioritize a particular frame or let the reconciler keep coherent motion from one image to avoid double edges.  
- **Color & Tone Consistency:** Minor exposure/white balance drift across a bracket is normalized before stacking. You can lock reference exposure to frame N and let others conform so the composite doesn’t exhibit banding or tone steps.

The UI reflects real production needs: import stacks by folder or drag-drop; auto-group by time gap; review thumbnails with sharpness heatmaps; toggle **Depth Preview** to visualize contributions; paint **in/out masks** for manual overrides; compare before/after with a split view. Export options include **16-bit TIFF**, **PNG**, **JPEG**, and **layered PSD** with depth map and contribution map embedded for downstream retouch. Naming tokens (`{set}`, `{index}`, `{fnumber}`, `{date}`, `{size}`) and **export recipes** accelerate delivery to clients or DAMs.

Performance is first class on modern Macs. The engine uses **vectorized kernels** and **Metal-accelerated** filters on Apple Silicon for near-instant previews and fast finals. Background queues let you keep editing while stacks render, and the **Job Manager** can batch multiple sets with per-set presets. Memory use is tuned for large stacks: tile streaming avoids exhausting RAM, and temporary files are pruned automatically after export.

Focus Stacker is opinionated about **safety and transparency**. It never alters your source images. Projects save as small descriptors referencing originals; if a session is interrupted, the app resumes with your parameters intact. A **provenance panel** lists alignment deltas, chosen metrics, blend levels, and any ghost regions you resolved—useful for QA, education, or repeatability in scientific imaging.

---

## 🧰 Features & Modules

| Module | What it does |
|---|---|
| Smart Align | Sub-pixel registration with breathing & minor perspective correction. |
| Depth Builder | Multi-metric focus confidence, edge-aware smoothing, and preview heatmaps. |
| Multi-Band Blend | Frequency-aware compositing to avoid halos and maintain micro-detail. |
| Ghost Resolver | Detects motion conflicts; choose a source frame for coherent regions. |
| Color Normalize | Unifies exposure/WB across the set; optional camera profile lock. |
| De-Halo & CA Guard | Suppress bright edge halos and color fringing at depth boundaries. |
| Retouch Brushes | Paint-in/out from specific frames; feather, flow, and edge detection. |
| Batch & Recipes | Auto-group stacks, apply presets, export multiple formats at once. |
| Exports | 16-bit TIFF/PNG/JPEG/PSD + depth and contribution maps; naming tokens. |
| Performance | Metal acceleration, tiled processing, background renders. |

---

## 🧪 Capture & Workflow Guide

**1) Capture best practices**  
- Use a **sturdy tripod** or macro rail; shoot electronic shutter if available.  
- Prefer **manual exposure**; set WB to a fixed value to avoid drift.  
- Step focus in **small, consistent increments**; overlap sharp zones generously.  
- Avoid f/22–f/32 diffraction; aim for **f/5.6–f/11** depending on magnification.  
- Lock lighting: constant LEDs/strobes; avoid mixed flicker sources.

**2) Import & group**  
- Drag a folder; auto-group by time gaps or filename increments.  
- Choose a preset (Macro, Product, Landscape, Scientific) to seed parameters.

**3) Align & inspect**  
- Run **Smart Align**; review the **Sharpness Heatmap** for coverage gaps.  
- If a subject moved, mark it as **ghost region** and pick a keeper frame.

**4) Build depth & blend**  
- Tune **window size** and **depth smoothing** for your texture type.  
- Enable **De-Halo/CA Guard** if you see bright edge glow or color fringing.

**5) Retouch & export**  
- Use **Paint-In** brush to borrow detail from a specific frame (e.g., specular edge).  
- Export **16-bit TIFF** for retouch + **web JPEG** using an export recipe.

---

## 🛠 Advanced Controls

- **Local Window Adaptation:** Auto-scales focus window by regional texture density.  
- **Detail Bias Slider:** Bias selection toward higher or lower frequency detail (helpful on fabrics vs. metal).  
- **Edge Priority:** Protects silhouette edges to avoid background bleed.  
- **Tone Lock:** Holds global tone curve to prevent low-frequency tone drift.  
- **Lens Breathing Profile:** Optional per-lens micro-scale curve for ultra-macro rails.  
- **Depth Map Export:** Save as grayscale EXR/PNG for 3D/relighting experiments.

---

## 🩹 Troubleshooting & Quality Tips

- **Wormy textures / halos:** Reduce detail bias, increase multi-band levels, enable De-Halo.  
- **Banding in gradients:** Increase depth smoothing and Tone Lock; ensure exposure normalization.  
- **Missed hairs/filaments:** Shrink window size locally and repaint from the best frame.  
- **Color seams:** Enable CA Guard; verify identical WB and profile on sources.  
- **Noise pickup in shadows:** Prefer the sharpest low-ISO frame for shadow regions using Paint-In.

---

## 🧾 File & Color Management

- Accepts: TIFF/PNG/JPEG (exported from RAW).  
- Color spaces: sRGB • Adobe RGB • ProPhoto RGB (preserved on export).  
- Metadata: EXIF/XMP (camera, lens, copyright, keywords) passed through.  
- PSD export: layered with **Depth** and **Contribution** maps.

---

## 🖼 Screenshots

![Workspace & Heatmap](https://static.macupdate.com/screenshots/333236/m/focus-stacker-screenshot.png?v=1649715974)

![Depth & Blending Controls](https://is1-ssl.mzstatic.com/image/thumb/Purple114/v4/bc/4b/55/bc4b5519-cfd0-c554-7838-599f960cc6c0/pr_source.png/643x0w.jpg)

![Batch Export Recipes](https://is1-ssl.mzstatic.com/image/thumb/Purple114/v4/99/12/22/991222b9-9868-5593-9fd6-007cdb34bc48/pr_source.png/643x0w.jpg)

---

## 🖥 System Requirements

| Parameter | Requirement |
|---|---|
| OS | macOS 10.14 (Mojave) or later |
| Mac | Apple Silicon (recommended) or Intel 64-bit |
| RAM | 8 GB minimum • 16–32 GB recommended for large stacks |
| Disk | SSD with free scratch space equal to **3×** largest stack |
| GPU | Metal-capable (Apple Silicon integrated or discrete AMD) |

---

## ❓ FAQ

**Do I need RAW files?**  
No—export 16-bit TIFFs (preferred) or high-quality JPEG/PNG from your RAW developer, then stack here.

**How many frames is ideal?**  
As many as needed to cover depth with overlap. Macro often uses 20–200; product 10–50; landscape 3–10.

**Can I stack handheld shots?**  
Yes; Smart Align compensates for small shifts. For critical work, use a tripod or rail.

**Why do I see halos?**  
They’re common at high-contrast depth boundaries. Enable De-Halo, increase blend bands, or retouch locally.

**Is it non-destructive?**  
Yes. Sources are never modified; sessions and parameters can be revisited any time.

---

## 🏷 Tags (SEO)

focus stacker mac • focus stacking software mac • macro focus stack • product photography stack • landscape focus blend • depth map blend mac • multi band blending macOS • macro rail focus breathing • ghost removal focus stack • de halo chromatic fringe • metal accelerated stacking • 16 bit tiff export mac • layered psd depth map • exif xmp preserve stack • apple silicon photo app • scientific imaging stack • jewelry watch macro sharp • pcb circuit board macro • food photography stack • tabletop product stack • photoshop affinity workflow • color managed stacking • sRGB adobe rgb prophoto • batch focus stacks mac • tripod handheld stacking
