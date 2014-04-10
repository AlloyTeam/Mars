Andorid Issues
==============
  <b><p>1. 三星I9100 （Android 4.0.4）不支持display:-webkit-flex这种写法的弹性布局，</p> 
         <p>但支持display:-webkit-box这种写法的布局, </p>
         <p>相关的属性也要相应修改，如-webkit-box-pack: center;</p>
         <p>移动端采用弹性布局时，建议直接写display:-webkit-box系列的布局</p>
         </b>
  <b><p>2. touchmove事件在Android部分机型(如LG Nexus 5 android4.4，小米2 android 4.1.1)上只会触发一次</p> 
         <p>解决方案是在触发函数里面加上e.preventDefault(); 记得将e也传进去。</p>
         </b>
