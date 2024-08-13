---
title: 解决pro-table的顶部搜索联动问题
date: 2024-08-13 11:44:07
tags:
  - "React"
  - "Ant_D"
categories:
  - "Ant_D"
keywords:
description: "pro-table根据前一项，改变下一项是下拉还是级联还是文本框的功能"
toc: false
---

## pro-table 根据前一项，改变下一项是下拉还是级联还是文本框的功能

![pro-table-search.gif](https://s2.loli.net/2024/08/13/SwRLioUscvB1upT.gif)

```js
const formRef = useRef();
const columns = [
  {
    title: "登记类型",
    dataIndex: "dengjileixing",
    align: "center",
    initialValue: null,
    valueType: "select",
    hideInTable: true,
    fieldProps: {
      options: [
        {
          value: "01",
          label: "综治件",
        },
        {
          value: "02",
          label: "司法件",
        },
        {
          value: "03",
          label: "法院件",
        },
      ], // 动态变量项
      allowClear: true,
      onChange: () => {
        formRef.current.setFieldsValue({
          jiefenleibie: null,
        });
      },
    },
  },
  {
    title: "纠纷类别",
    dataIndex: "jiefenleibie",
    align: "center",
    initialValue: null,
    hideInTable: true,
    renderFormItem: (
      _,
      { type, defaultRender, formItemProps, fieldProps, ...rest },
      form
    ) => {
      if (type === "form") {
        return null;
      }
      const dengjileixing = form.getFieldValue("dengjileixing");
      if (dengjileixing === "03") {
        return (
          <Cascader
            allowClear
            style={{ width: "100%" }}
            options={[
              {
                value: "zhejiang",
                label: "Zhejiang",
                children:[
                  {
                    value: "hangzhou",
                    label: "Hangzhou",
                    children: [
                      {
                        value: "xihu",
                        label: "West Lake",
                      },
                    ],
                  },
                ],
              },
            ]}
            placeholder="纠纷类别"
          />
        );
      } else if (dengjileixing === "01" || dengjileixing === "02") {
        return (
          <Select
            allowClear
            style={{ width: "100%" }}
            options={[
              { value: "jack", label: "Jack" },
              { value: "lucy", label: "Lucy" },
            ]}
            placeholder="纠纷类别"
          />
        );
      } else {
        return <Input disabled placeholder="纠纷类别" />;
      }
    },
  },
];

<ProTable
  rowKey="id"
  columns={columns}
  formRef={formRef}
  request={requestList}
  actionRef={tableRef}
  options={false}
  tableAlertRender={false}
/>;
```
