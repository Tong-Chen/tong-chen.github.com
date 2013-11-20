---
title: How to identify a research problem
author: 悟道
layout: post
permalink: /?p=3196
categories:
  - 转载
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div>
  <strong>My Story at Princeton</strong>
</div>

I just completed the PARSEC project and started to look for new research projects. I came up with an idea that I planned to work on for 2~3 years with a group of 3~5 students. I discussed the idea with <a href="http://www.cs.princeton.edu/%7Eli/" target="_blank">Prof. Kai Li</a> and asked for his advice.

<div>
  I originally thought that Kai would like the idea, but he gave me unexpected feedback. He said that the project is too ambitious to be finished by just one person in a short time. Furthermore, from the methodology perspective, usually, there is only one best solution for one specific goal. My idea violated the natural rule that achieving three goals by doing just one thing. He suggested me to firstly look for an idea that I can make progress on in three months.
</div>

<div>
</div>

<div>
  I had to admit that I was stunned by hearing the comment that was not supposed to be spoken out from Kai&#8217;s mouth. I used to hear him talk about how to identify a research topic when I was in ICT several years ago. He disagreed with the way ICTers do research projects whose goals are to prudently complete the requirements of proposals. He told ICTers that you need to setup ambitious research projects aiming at global demands and  you also want to tolerate failure since good research implies high risk.
</div>

<div>
</div>

<div>
  In his office, he kept talking about his opinion, experience as well as some concrete examples. He said, &#8220;if you devote yourself on a long-term project when you are just a junior faculty, you would probably not get any publications for a while, then some issues will show off. You might encounter doubt. People will doubt you. Especially in China, there is performance review every year. So you need to escalate your confidence through the progress of a series of short-term projects.&#8221;. He added, &#8220;this proposal is sort of inappropriate but I&#8217;m not gonna to criticize you. Actually this is a good exercise. You can learn how to identify proper projects from these lessons.&#8221;
</div>

<div>
</div>

<div>
  After I walked out from Kai&#8217;s office, I reflected on my original way of doing research. It seems that I always come up with a bunch of rough ideas but never refine those ideas to several concrete challenges. Thus, I always propose kind of big projects. How to identify a proper idea? In fact, finding an idea means finding a good problem. I think there should be several common steps.
</div>

<div>
</div>

<div>
</div>

<div>
  <strong>An overview of Research Flow</strong>
</div>

<div>
</div>

<div>
  The following chart illustrates my understanding of how to carry on research.
</div>

![][1]

&nbsp;

**Case Studies**

<div>
  <div>
  </div>
  
  <div>
    Let&#8217;s look at two case studies.
  </div>
  
  <div>
  </div>
  
  <div>
    1. Dr. <a href="http://web.eecs.umich.edu/%7Exyzhang/" target="_blank">Xinyu Zhang</a> wrote an article on how he did the research that ended up with ACM MobiCom 2011 best paper award (&#8220;<a href="http://blog.sciencenet.cn/home.php?mod=space&uid=44406&do=blog&id=490483" target="_blank">获得ACM MobiCom 2011 最佳论文奖</a>&#8220;,科学网). I drew the diagram to describe his experience according to the article.
  </div>
  
  <div>
  </div>
  
  <div>
    In 2008, Xinyu took a course on real system and learned the idea of DVFS that is widely used in microprocessor. He asked a question that &#8220;why not apply DVFS to wireless receiver?&#8221;. After doing survey and thinking, he found the reason that wireless receiver is required to obey Nyquist-Shannon Sampling Theorem in order to correctly receive and decode signals. It seems impossible to break the theorem, so he thought the idea was not doable. But in 2010, one day when he was reading papers, he suddenly came up with a solution that receiving and decoding can be decoupled. Then, he quickly implemented his idea and verified its feasibility. Finally, this work won the ACM Mobicom 2011 best paper award which led him to be a faculty of University of Wisconsin Madison.
  </div>
  
  <div>
  </div>
  
  <div>
    In Xinyu&#8217;s story, I think the key reason he succeeded is that he had distilled the key challenge in 2008.
  </div>
  
  <div>
  </div>
  
  <div>
    <img alt="" src="http://blog.sciencenet.cn/static/ueditor/themes/default/images/spacer.gif" /><img alt="" src="http://image.sciencenet.cn/album/201307/08/230034z9npchcagbwhy33i.png" />
  </div>
  
  <div>
  </div>
  
  <div>
  </div>
  
  <div>
    2. Prof. Kai Li was elected as a member of the National Academy of Engineering in 2012 for his contributions in the fields of data storage and distributed computer systems. Kai pioneered the distributed shared memory (DSM) techniques that allow users to program using a shared-memory programming model on clusters of computers.
  </div>
  
  <div>
  </div>
  
  <div>
    I used to ask Kai how he came up with the great idea, and he answered that originally he was working on implementing a message-based programming model by RPC that was just proposed in the early 1980s. But he struggled with handling pointers between different machines. So he asked a question that &#8220;why not use global address space in the distributed system?&#8221;.  He delved into the question and found that the key challenge was how to maintain data coherence among multiple machines. He borrowed the idea of CPU cache coherence protocol and applied it to DSM. Actually, his prestigious paper on DSM is entitled &#8220;memory coherence in shared virtual memory systems&#8221;, which has been cited by more than 1600 times.
  </div>
  
  <div>
  </div>
  
  <div>
    Kai&#8217;s story exemplifies the importance of distilling key challenges after coming up with a rough new idea.
  </div>
  
  <div>
  </div>
  
  <div>
    <img alt="" src="http://image.sciencenet.cn/album/201307/08/2300412gv9v2vf9s92b0ff.png" />
  </div>
  
  <p>
    &nbsp;
  </p>
  
  <p>
    <img alt="" src="http://blog.sciencenet.cn/static/ueditor/themes/default/images/spacer.gif" />
  </p>
  
  <div>
    <div>
      <div>
        Actually, &#8220;how to do good research?&#8221; Perhaps this is the question that every researcher used to ask himself or herself. This article presents my thought and understanding on how to do good research. Be cautious that I am a good researcher yet but just a junior guy. You comments are welcome.
      </div>
    </div>
  </div>
  
  <p>
    http://blog.sciencenet.cn/blog-414166-706460.html
  </p>
</div>

 [1]: http://image.sciencenet.cn/album/201307/08/230025knkx3h9om9knz39h.png