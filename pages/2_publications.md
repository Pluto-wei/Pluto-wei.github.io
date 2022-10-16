---
layout: page
title: Publications
comments: true
permalink: /publications/

---

* content
{:toc}

<style>
.biblist { }
/* The item */
.biblist li { }

/* You can define custom styles for plstyle field here. */

/*************************************
   The box that contain BibTeX code
 *************************************/
div.noshow { display: none; }
div.BibTeX {
  margin-right: 1%;
  margin-left: 3%;
  margin-top: 1.2em;
  margin-bottom: 1.3em;
  border: 1px solid silver;
  padding: 0.3em 0.5em;
  background: #eeeeee;
}
div.BibTeX pre { font-size: 100%; overflow: auto;  width: 100%; }
</style>

<script>
function toggleBibtex(articleid) {
  var bib = document.getElementById('bib_'+articleid);
  if (bib) {
    if(bib.className.indexOf('BibTeX') != -1) {
    bib.className.indexOf('noshow') == -1?bib.className = 'BibTeX noshow':bib.className = 'BibTeX';
    }
  } else {
    return;
  }
}
</script>
# Publications

## 2022

* **Yu-Wei Zhuo**, Tian-Jing Zhang, Jin-Fan Hu, Hong-Xia Dou, Ting-Zhu Huang and Liang-Jian Deng. "A Deep-Shallow Fusion Network with Multi-Detail Extractor and Spectral Attention for Hyperspectral Pansharpening." **IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing (IEEE JSTARS)**. [[Project Page]](https://github.com/liangjiandeng/Hyper-DSNet) [[DOI]](https://ieeexplore.ieee.org/document/9870551/) [[PDF]](https://pluto-wei.github.io/papers/2022/zhuo-jstars2022.pdf) <a href="javascript:toggleBibtex('zhuo2022jstars')" class="textlink">[BibTeX]</a>
<div id="bib_zhuo2022jstars" class="BibTeX noshow">
<pre>
@ARTICLE{zhuo2022jstars,
  	title={A Deep-Shallow Fusion Network With Multidetail Extractor and Spectral Attention for Hyperspectral Pansharpening},
  	author={Zhuo, Yu-Wei and Zhang, Tian-Jing and Hu, Jin-Fan and Dou, Hong-Xia and Huang, Ting-Zhu and Deng, Liang-Jian},
  	journal={IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing},
  	volume={15},
  	pages={7539--7555},
  	year={2022},
  	publisher={IEEE}
}
</pre>
</div>



* Zi-Rong Jin#, **Yu-Wei Zhuo#**, Tian-Jing Zhang, Xiao-Xu Jin and Liang-Jian Deng.“Parallel Full Depth Feature Fusion Network for Pansharpening.” ***Remote Sensing***. (#: equal contribution) [[DOI]](https://doi.org/10.3390/rs14030466) [[PDF]](https://pluto-wei.github.io/papers/2022/jin-remote2022.pdf) <a href="javascript:toggleBibtex('jin2022remote')" class="textlink">[BibTeX]</a>

<div id="bib_jin2022remote" class="BibTeX noshow">
<pre>
@article{jin2022remote,
  title={Remote Sensing Pansharpening by Full-Depth Feature Fusion},
  author={Jin, Zi-Rong and Zhuo, Yu-Wei and Zhang, Tian-Jing and Jin, Xiao-Xu and Jing, Shuaiqi and Deng, Liang-Jian},
  journal={Remote Sensing},
  volume={14},
  number={3},
  pages={466},
  year={2022},
  publisher={MDPI}
}
</pre>
</div>



* Si-Ran Peng, Liang-Jian Deng, Jin-Fan Hu and **Yu-Wei Zhuo**. "Source-Adaptive Discriminative Kernels based Network for Remote Sensing Pansharpening." ***International Joint Conferences on Artificial Intelligence (IJCAI-2022)*** [[DOI]](https://www.ijcai.org/proceedings/2022/179) [[PDF]](https://pluto-wei.github.io/papers/2022/peng-ijcai2022.pdf) <a href="javascript:toggleBibtex('pengijcai2022')" class="textlink">[BibTeX]</a> [[Code]](https://github.com/liangjiandeng/ADKNet)

<div id="bib_pengijcai2022" class="BibTeX noshow">
<pre>
@ARTICLE{pengijcai2022,
	author={Peng, Si-ran and Deng, Liang-Jian and Hu, Jin-Fan and Zhuo, Yu-wei},
	journal={International Joint Conferences on Artificial Intelligence (IJCAI)}, 
	title={Source-Adaptive Discriminative Kernels based Network for Remote Sensing Pansharpening}, 
	year={2022},
	volume={},
	number={},
	pages={},
	doi={}
   }
</pre>
</div>







