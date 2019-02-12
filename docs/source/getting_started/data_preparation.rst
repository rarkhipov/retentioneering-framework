Download data
=============

Firstly, you should export your clickstream data as csv or other table
format (also, you can download data directly from
`BigQuery <bigquery.md>`__).

Data should have at least three columns: ``user_id``,
``event_timestamp`` and ``event_name``.

Prepare data for analysis
=========================

Firstly, openning data in python is needed

.. code:: python

    import pandas as pd
    data = pd.read_csv('path_to_your_data.csv')

You also can read data from other sources such as ``.xlsx``
(``pd.read_excel``), ``sql`` (``pd.read_sql``) and etc. Please, check
the `pandas
documentation <https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html>`__
for other options

Columns renaming and formatting
-------------------------------

Analysis submodule need proper names of columns:

1. User id should be named as ``user_pseudo_id``
2. Name of event should be ``event_name``
3. Timestamp of event should be ``event_timestamp``. Also it is needed
   to convert it to the integer (seconds from ``1970-01-01``).

Rename your columns with pandas

.. code:: python

    data = data.rename({
        'your_user_id_column_name': 'user_pseudo_id',
        'your_event_name_column_name': 'event_name',
        'your_event_timestamp_name': 'event_timestamp'
    }, axis=1)

Check your timestamp type

.. code:: python

    print("""
    Event timestamp type: {}
    Event timestamp example: {}
    """.format(
        data.event_timestamp.dtype,
        data.event_timestamp.iloc[0]
    ))

Out:

.. code:: none

    Event timestamp type: obj
    Event timestamp example: 2019-02-09 16:10:23

The event timestamp here is python object (string).

You can convert it to seconds with following code

.. code:: python

    # converts string to datetime 
    data.event_timestamp = pd.to_datetime(data.event_timestamp)

    # converts datetime to integer
    data.event_timestamp = data.event_timestamp.astype(int) / 1e6

Add target events
-----------------

Most of our tools aims to estimate how different trajectories leads to
different target events. So it could be needed to add such events as
``lost`` and ``passed``.

For example, there is a list of events that corresponds to passed
onboarding.

.. code:: python

    from retentioneering import preparing
    event_filter = ['newFlight', 'feed', 'tabbar', 'myFlights']
    data = preparing.add_passed_event(data, positive_event_name='passed', filter=event_filter)

And all who was not passed over some time is lost

.. code:: python

    data = preparing.add_lost_event(data, existed_event='pass', time_thresh=5)

Export data
-----------

.. code:: python

    data.to_csv('prepared_data.csv', index=False)

