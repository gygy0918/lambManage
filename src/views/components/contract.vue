<template>
  <div >
    <div id="container" style="width:500px; height:300px"></div>

  </div>
</template>
<script>
  import AMap from 'AMap'
  var map
  export default {
    mounted: function () {
      this.init()
    },
    methods: {
    //显示地图加控件
      init: function () {
              var map = new AMap.Map('container', {
                  pitch:75,
                  viewMode:'3D',
                  zoom: 19,
                  expandZoomRange:true,
                  zooms:[3,20],
                  center:[116.35636,39.960378]
                });
                map.plugin(["AMap.ToolBar"], function() {
                      map.addControl(new AMap.ToolBar());
                  });
var markers = [];   
//provinces见Demo引用的JS文件
var provinces=[["116.4123","39.906422"],["116.4352","39.906933"],["116.445435","39.9054345"]];
for(var i = 0; i < provinces.length; i += 1){
    //TODO 根据类别创建不同样式的marker
    marker = new AMap.Marker({
position: provinces[i].center.split(','),
map: map
    });
}









        AMap.service('AMap.Geocoder',function(){//回调函数
    //实例化Geocoder
    var geocoder = new AMap.Geocoder({
        city: "010"//城市，默认：“全国”
    });
    //TODO: 使用geocoder 对象完成相关功能
        //逆地理编码
        var lnglatXY=[116.396574, 39.992706];//地图上所标点的坐标
    geocoder.getLocation("北京市海淀区西土城十号北京邮电大学", function(status, result) {
    if (status === 'complete' && result.info === 'OK') {
        //TODO:获得了有效经纬度，可以做一些展示工作
        //比如在获得的经纬度上打上一个Marker
        console.log(result.geocodes)
    }else{
        //获取经纬度失败
    }
});   
})

      }
    }
  }
</script>
<style>
</style>