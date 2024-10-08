# How to use graphs

This guide shows you how to use graphs to visualize your data in the dashboard.

The [`Graph`][vizro.models.Graph] model is the most used component in many dashboards, allowing you to visualize data in a variety of ways.

To add a [`Graph`][vizro.models.Graph] to your page, do the following:

- insert the [`Graph`][vizro.models.Graph] model into the `components` argument of the
[`Page`][vizro.models.Page] model
- enter any of the currently available charts of the open source library [`plotly.express`](https://plotly.com/python/plotly-express/) into the `figure` argument

!!! note

    In order to use the [`plotly.express`](https://plotly.com/python/plotly-express/) chart in a Vizro dashboard, you need to import it as `import vizro.plotly.express as px`.
    This leaves any of the [`plotly.express`](https://plotly.com/python/plotly-express/) functionality untouched, but allows _direct insertion_ into the [`Graph`][vizro.models.Graph] model _as is_.

    Note also that the `plotly.express` chart needs to have a `data_frame` argument. In case you require a chart without
    a `data_frame` argument (for example, the [`imshow` chart](https://plotly.com/python/imshow/)), refer to our
    [guide on custom charts](custom-charts.md).



!!! example "Graph"
    === "app.py"
        ```{.python pycafe-link}
        import vizro.models as vm
        import vizro.plotly.express as px
        from vizro import Vizro

        df = px.data.iris()

        page = vm.Page(
            title="My first page",
            components=[
                vm.Graph(
                    figure=px.scatter_matrix(
                        df, dimensions=["sepal_length", "sepal_width", "petal_length", "petal_width"], color="species"
                    ),
                ),
            ],
        )

        dashboard = vm.Dashboard(pages=[page])

        Vizro().build(dashboard).run()
        ```
    === "app.yaml"
        ```yaml
        # Still requires a .py to add data to the data manager and parse YAML configuration
        # See yaml_version example
        pages:
        - components:
          - figure:
              _target_: scatter_matrix
              color: species
              data_frame: iris
              dimensions: ["sepal_length", "sepal_width", "petal_length", "petal_width"]
            type: graph
          title: My first page
        ```
    === "Result"
        [![Graph]][Graph]

    [Graph]: ../../assets/user_guides/components/graph.png


In the Python example we directly inserted the pandas DataFrame `df` into `figure=px.scatter_matrix(df, ...)`. This is [one way to supply data to a chart](data.md#supply-directly). For the YAML version, we [refer to the data source by name](data.md#reference-by-name) as `data_frame: iris`. For a full explanation of the different methods you can use to send data to your dashboard, see [our guide to using data in Vizro](data.md).

## Add title, header, footer

To enhance your `Graph` with a title, header, or footer to provide additional context or descriptions,
refer to our detailed user guide on [title, header, and footer](title-header-footer.md).
