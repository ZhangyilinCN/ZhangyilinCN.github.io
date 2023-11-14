---
title: '多图重叠带icon的柱形图'
date: 2023-11-14 11:19:15
tags:
  - 'React'
  - 'Echarts'
categories:
  - 'Echarts'
keywords:
description: '使用react和echarts构建较为复杂的多图重叠的柱形图'
toc: false
---

**直接上效果图**

![echarts_pic_20231114.png](https://s2.loli.net/2023/11/14/ecZrgQXa8Bl9kqT.png)

**代码如下**

``` js
/* eslint-disable react/no-array-index-key */
import React, { useRef, useState, useEffect } from 'react';
import * as echarts from 'echarts';
import styles from './charts.less';

const REMNUM = parseFloat(window.sessionStorage.getItem('remNum') || 20)

const colorsList = [
    '147, 255, 180',
    '255, 165, 21',
    '2, 161, 255',
    '68, 93, 255',
    '98, 0, 255'
]
const options = {
    grid: {
        top: "18%",
        left: "10%",
        right: "5%",
        bottom: "12%",
    },
    tooltip: {
        trigger: 'axis',
        axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
        },
    },
    legend: {
        type: 'scroll',
        pageIconColor: '#76b9ff',
        pageIconInactiveColor: 'yellow',
        pageTextStyle: {
            color: '#76b9ff',
            fontSize: 1 * REMNUM,
        },
        top: '0',
        itemGap: 0.75 * REMNUM,
        itemWidth: 1 * REMNUM,
        itemHeight: 1 * REMNUM,
        icon: 'path://M512 951.6c-20.1 0-39.4-8-53.7-22.2L94.6 565.7C65 536 65 488 94.6 458.3L458.3 94.6C488 65 536 65 565.7 94.6l363.7 363.7c14.2 14.2 22.2 33.5 22.2 53.7 0 20.1-8 39.4-22.2 53.7L565.7 929.4c-14.3 14.2-33.6 22.2-53.7 22.2zM255.6 512L512 768.4 768.4 512 512 255.6 255.6 512z',
        textStyle: {
            color: '#98bbff',
            fontSize: 0.8 * REMNUM,
        },
        data: null
    },
    calculable: true, // 可计算特性
    xAxis: [
        {
            type: 'category',
            data: null,
            axisLine: {
                lineStyle: {
                    color: "rgb(29,74,129)",
                },
            },
            axisLabel: {
                color: "#98bbff",
                textStyle: {
                    fontSize: 0.7 * REMNUM,
                },
            },
            splitLine: {
                show: false,
            },
            axisTick: {
                show: false,
            },
        }
    ],
    yAxis: [
        {
            type: 'value',
            axisLine: {
                show: false,
            },
            splitLine: {
                show: true,
                lineStyle: {
                    color: 'rgb(10,31, 72)'
                },
            },
            axisLabel: {
                color: "#98bbff",
                textStyle: {
                    fontSize: 0.7 * REMNUM,
                },
            },
            axisTick: {
                show: false,
            },
        }
    ],
    series: null
};

// const chartData = [
//     {
//         name: '1月',
//         value: [
//             { name: 'AA', value: 77 },
//             { name: 'BB', value: 66 },
//             { name: 'CC', value: 55 },
//         ]
//     },
//     {
//         name: '2月',
//         value: [
//             { name: 'AA', value: 7 },
//             { name: 'BB', value: 6 },
//             { name: 'CC', value: 5 },
//         ]
//     }
//     ........
// ]

const LineEcharts = ({ chartData }) => {
    const echartRef = useRef(null)
    const [chart, setChart] = useState(null)
    // 初始化ecart
    const initEchartFn = (arr) => {
        let myChart = chart
        if (!chart) {
            const chartDom = echartRef.current
            myChart = echarts.init(chartDom);
            setChart(myChart)
            myChart.on('legendselectchanged', (params) => {
                const selectItemArr = []
                // eslint-disable-next-line no-restricted-syntax
                for (const k in params.selected) {
                    if (params.selected[k]) {
                        selectItemArr.push(k)
                    }
                }
                // eslint-disable-next-line no-use-before-define
                setEchartsOptionsFn(myChart, arr, selectItemArr)
            })
        }
        // eslint-disable-next-line no-use-before-define
        setEchartsOptionsFn(myChart, arr)
    }
    const setEchartsOptionsFn = (myChart, arr, selectItemArr) => {
        const arrLen = arr.length || 0
        const sumArr = []
        arr.forEach(item => {
            item.value.forEach((item2, index2) => {
                if (!sumArr[index2]) {
                    sumArr[index2] = { name: item2.name, arr: [item2.value] }
                } else {
                    sumArr[index2].arr = [...sumArr[index2].arr, item2.value]
                }
            })
        })
        const seriesArr1 = sumArr.map((item, index) => {
            const itemObj = {
                name: item.name,
                type: 'bar',
                stack: 'barEcharts',
                data: item.arr,
                itemStyle: {
                    normal: {
                        color: new echarts.graphic.LinearGradient(
                            0, 1, 0, 0, [
                            {
                                offset: 1,
                                color: `rgba(${colorsList[index]}, 0.6)`
                            },
                            {
                                offset: 0,
                                color: `rgba(${colorsList[index]}, 0.3)`
                            }
                        ]
                        ),
                    }
                },
            }
            return itemObj
        })
        let zancunArr = []
        let newSumArr = JSON.parse(JSON.stringify(sumArr))
        if (selectItemArr) {
            newSumArr = newSumArr.map(item => {
                const newArrItem = selectItemArr.filter(item2 => {
                    return item.name === item2
                })
                if (newArrItem?.length) {
                    return item
                }
                return { ...item, arr: [] }

            })
        }
        const seriesOldArr = newSumArr.map((item, index) => {
            if (!index) {
                const arrItem = JSON.parse(JSON.stringify(item.arr))
                zancunArr = arrItem
                return arrItem
            }
            let newItemArr2 = JSON.parse(JSON.stringify(item.arr))
            if (!newItemArr2.length) {
                newItemArr2 = new Array(arrLen + 10).fill(0)
            }
            const newArr3 = newItemArr2.map((item2, index2) => {
                return item2 + (zancunArr[index2] || 0)
            })
            zancunArr = JSON.parse(JSON.stringify(newArr3))
            return newArr3
        })
        const zhanbiNumStr = `${100 - ((seriesOldArr.length - 1) * 5)}%`
        const seriesArr2 = seriesOldArr.map((item, index) => {
            return (
                {
                    type: 'pictorialBar',
                    data: item.length > arrLen ? [] : item,
                    xAxisIndex: 0,
                    yAxisIndex: 0,
                    zlevel: 99,
                    symbol: "rect",
                    symbolSize: [zhanbiNumStr, 0.3 * REMNUM],
                    symbolPosition: 'end',
                    symbolOffset: [0, 0],
                    itemStyle: {
                        color: `rgb(${colorsList[index]})`,
                    },
                }
            )
        })
        const maxLen = seriesArr1.length
        options.tooltip.formatter = (params) => {
            let newArr = null;
            if (selectItemArr?.length) {
                newArr = params.flatMap(item => {
                    const newsItem = selectItemArr.filter(item2 => {
                        return item2 === item.seriesName
                    })
                    if (newsItem?.length) {
                        return item
                    }
                    return []
                })
            } else {
                newArr = params
            }
            const firstStr = `${newArr[0].name}`
            const newStrArr = newArr.flatMap((item, index) => {
                if (index < maxLen) {
                    return (
                        `<br />${item.marker}${item.seriesName}:${item.data}`
                    )
                }
                return []
            })
            return firstStr + newStrArr.join('')

        }
        options.legend.data = arr[0].value.map(item => item.name)
        options.xAxis[0].data = arr.map(item => item.name)
        options.series = [...seriesArr1, ...seriesArr2]
        myChart.setOption(options);
    }
    // 自适应
    const echartsResize1 = () => {
        if (echartRef.current) {
            echarts.init(echartRef.current).resize();
        }
    }
    useEffect(() => {
        initEchartFn(chartData)
    }, [chartData])
    // 监听echartsResize函数，实现图表自适应
    window.addEventListener('resize', echartsResize1);
    useEffect(() => {
        // 页面卸载，销毁监听
        return () => {
            window.removeEventListener('resize', echartsResize1);
        }
    }, [])
    return (
        <div className={styles.bar_echart_wrap}>
            <div className={styles.bar_dom} ref={echartRef} />
        </div>
    );
};
export default LineEcharts

```




