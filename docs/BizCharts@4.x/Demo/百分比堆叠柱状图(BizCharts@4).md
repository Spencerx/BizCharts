# 百分比堆叠柱状图(BizCharts@4)

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/e2ebbd00-aee7-11ea-af03-e39c6df319e0.png)

```js
import React from "react";
import DataSet from '@antv/data-set';
import {
  G2,
  Chart,
  Tooltip,
  Interval,
  Coord
} from "bizcharts";

const data = [
  { country: 'Europe', year: '1750', value: 163 },
  { country: 'Europe', year: '1800', value: 203 },
  { country: 'Europe', year: '1850', value: 276 },
  { country: 'Europe', year: '1900', value: 408 },
  { country: 'Europe', year: '1950', value: 547 },
  { country: 'Europe', year: '1999', value: 729 },
  { country: 'Europe', year: '2050', value: 628 },
  { country: 'Europe', year: '2100', value: 828 },
  { country: 'Asia', year: '1750', value: 502 },
  { country: 'Asia', year: '1800', value: 635 },
  { country: 'Asia', year: '1850', value: 809 },
  { country: 'Asia', year: '1900', value: 947 },
  { country: 'Asia', year: '1950', value: 1402 },
  { country: 'Asia', year: '1999', value: 3634 },
  { country: 'Asia', year: '2050', value: 5268 },
  { country: 'Asia', year: '2100', value: 7268 },
];


function Grouped() {
  // 计算每个柱子的占比
  const ds = new DataSet();
  const dv = ds
    .createView()
    .source(data)
    .transform({
      type: 'percent',
      field: 'value', // 统计销量
      dimension: 'country', // 每年的占比
      groupBy: ['year'], // 以不同产品类别为分组
      as: 'percent',
    });
  return (
    <Chart
      height={400}
      padding="auto"
      scale={{
        percent: {
          min: 0,
          formatter(val) {
            return (val * 100).toFixed(2) + '%';
          },
        }
      }}
      data={dv.rows}
      autoFit
    >
      <Interval
        adjust="stack"
        color="country"
        position="year*percent"
      />
      <Tooltip shared />
    </Chart>
  );
}

ReactDOM.render(<Grouped />, mountNode)

```
