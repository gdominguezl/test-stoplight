---
stoplight-id: arr7uux831va0
---

# Chart Types in API Endpoints

> ### **Description:**
> 
> In this document, we outline the proposed data structures for various chart types that may be returned in API endpoint JSON responses. These structures are designed to be easily rendered into corresponding charts on the frontend.
> 
> Our backend (Nest JS) will receive the raw data, process it, and convert it into the appropriate format to match the chart structures proposed in this document. This ensures a seamless integration between the data received from the API and the chart components on the frontend.

---

## **Line charts**

![Screen Shot 2023-05-07 at 17.57.21.png](<../../../assets/images/Screen Shot 2023-05-07 at 17.57.21.png>)

**Proposed JSON structure:**
```json
{
  "chartType": "line",
  "title": "<title>",
  "xAxisTitle": "<x_axis_title>",
  "yAxisTitle": "<y_axis_title>",
  "data": [
    {
      "label": "<label_for_variable_1>",
      "color": "<color_1>",
      "unit": "<unit_1>",
      "values": [
        {
          "x": "<x_value_1>",
          "y": "<y_value_1>"
        },
        // ... Additional data points for variable 1
      ]
    },
    {
      "label": "<label_for_variable_2>",
      "color": "<color_2>",
      "unit": "<unit_2>",
      "values": [
        {
          "x": "<x_value_2>",
          "y": "<y_value_2>"
        },
        // ... Additional data points for variable 2
      ]
    },
    {
      "label": "<label_for_variable_3>",
      "color": "<color_3>",
      "unit": "<unit_3>",
      "values": [
        {
          "x": "<x_value_3>",
          "y": "<y_value_3>"
        },
        // ... Additional data points for variable 3
      ]
    }
  ]
}

```


## **Bar charts**

![Screen Shot 2023-05-09 at 07.42.47.png](<../../../assets/images/Screen Shot 2023-05-09 at 07.42.47.png>)


**Proposed JSON structure:**
```json
{
  "chartType": "bar",
  "title": "<title>",
  "xAxisTitle": "<x_axis_title>",
  "yAxisTitle": "<y_axis_title>",
  "xAxisLabels": ["<x_axis_label_1>", "<x_axis_label_2>", "<x_axis_label_3>", "<x_axis_label_4>"],
  "yAxisLabels": ["<y_axis_label_1>", "<y_axis_label_2>", "<y_axis_label_3>", "<y_axis_label_4>", "<y_axis_label_5>"],
  "data": [
    {
      "label": "<label_for_variable>",
      "unit": "<unit>",
      "values": [
        {
          "x": "<x_value_1>",
          "y": "<y_value_1>"
        },
        {
          "x": "<x_value_2>",
          "y": "<y_value_2>"
        },
        {
          "x": "<x_value_3>",
          "y": "<y_value_3>"
        },
        {
          "x": "<x_value_4>",
          "y": "<y_value_4>"
        }
      ]
    }
  ]
}
```

## **Grouped bar charts**

![Screen Shot 2023-05-07 at 17.47.23.png](<../../../assets/images/Screen Shot 2023-05-07 at 17.47.23.png>)

![Screen Shot 2023-05-07 at 17.48.15.png](<../../../assets/images/Screen Shot 2023-05-07 at 17.48.15.png>)

**Proposed JSON structure:**

```json
{
  "chartType": "groupedBar",
  "title": "<title>",
  "xAxisTitle": "<x_axis_title>",
  "yAxisTitle": "<y_axis_title>",
  "xAxisLabels": ["<x_axis_label_1>", "<x_axis_label_2>", "<x_axis_label_3>", "<x_axis_label_4>"],
  "yAxisLabels": ["<y_axis_label_1>", "<y_axis_label_2>", "<y_axis_label_3>", "<y_axis_label_4>", "<y_axis_label_5>"],
  "data": [
    {
      "label": "<label_for_dimension_1>",
      "unit": "<unit_1>",
      "values": [
        {
          "x": "<x_value_1>",
          "y": "<y_value_1>"
        },
        {
          "x": "<x_value_2>",
          "y": "<y_value_2>"
        },
        {
          "x": "<x_value_3>",
          "y": "<y_value_3>"
        },
        {
          "x": "<x_value_4>",
          "y": "<y_value_4>"
        }
      ]
    },
    {
      "label": "<label_for_dimension_2>",
      "unit": "<unit_2>",
      "values": [
        {
          "x": "<x_value_5>",
          "y": "<y_value_5>"
        },
        {
          "x": "<x_value_6>",
          "y": "<y_value_6>"
        },
        {
          "x": "<x_value_7>",
          "y": "<y_value_7>"
        },
        {
          "x": "<x_value_8>",
          "y": "<y_value_8>"
        }
      ]
    }
  ]
}
```

## **Grouped bar charts with line (Three dimensions grouped bar)**

![Screen Shot 2023-05-07 at 17.49.01.png](<../../../assets/images/Screen Shot 2023-05-07 at 17-2.49.01.png>)

![Screen Shot 2023-05-07 at 17.49.10.png](<../../../assets/images/Screen Shot 2023-05-07 at 17.49.10.png>)

![Screen Shot 2023-05-07 at 17.50.13.png](<../../../assets/images/Screen Shot 2023-05-07 at 17.50.13.png>)

**Proposed JSON structure:**

```json
{
  "chartType": "groupedBarWithLine",
  "title": "<title>",
  "xAxisTitle": "<x_axis_title>",
  "yAxisTitle": "<y_axis_title>",
  "xAxisLabels": ["<x_axis_label_1>", "<x_axis_label_2>", "<x_axis_label_3>", "<x_axis_label_4>"],
  "yAxisLabels": ["<y_axis_label_1>", "<y_axis_label_2>", "<y_axis_label_3>", "<y_axis_label_4>", "<y_axis_label_5>", "<y_axis_label_6>"],
  "data": [
    {
      "label": "<label_for_dimension_1 (First variable)>",
      "unit": "<unit_1>",
      "values": [
        {
          "x": "<x_value_1>",
          "y": "<y_value_1>"
        },
        {
          "x": "<x_value_2>",
          "y": "<y_value_2>"
        },
        {
          "x": "<x_value_3>",
          "y": "<y_value_3>"
        },
        {
          "x": "<x_value_4>",
          "y": "<y_value_4>"
        }
      ]
    },
    {
      "label": "<label_for_dimension_2 (Second variable)>",
      "unit": "<unit_2>",
      "values": [
        {
          "x": "<x_value_5>",
          "y": "<y_value_5>"
        },
        {
          "x": "<x_value_6>",
          "y": "<y_value_6>"
        },
        {
          "x": "<x_value_7>",
          "y": "<y_value_7>"
        },
        {
          "x": "<x_value_8>",
          "y": "<y_value_8>"
        }
      ]
    },
    {
      "label": "<label_for_dimension_3 (Third variable - the line on the graph)>",
      "unit": "<unit_3>",
      "type": "<type>",
      "values": [
        {
          "x": "<x_value_9>",
          "y": "<y_value_9>"
        },
        {
          "x": "<x_value_10>",
          "y": "<y_value_10>"
        },
        {
          "x": "<x_value_11>",
          "y": "<y_value_11>"
        },
        {
          "x": "<x_value_12>",
          "y": "<y_value_12>"
        }
      ]
    }
  ]
}
```
