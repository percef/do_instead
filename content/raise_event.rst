Programming on anvil.works
###########################
:tags: client
:category: anvil.works
:summary: Use raise_event only on simplest parent-child forms.
:date: 2021-11-19 10:36
:slug: raise-event

raise_event on Multiple Hierarchy: Run Away!
============================================
Run away from  `set_event_handler` and `raise_event`. Use these only for the simplest events.

Instead
===========

`Anvil Extras <https://anvil-extras.readthedocs.io/en/latest/guides/modules/messaging.html>`_
has a module called **Messaging** that will allow events to trigger handles anywhere on the app.

In a separate file: `global_vars.py`, put::

    from anvil_extras.messaging import Publisher
    publisher = Publisher(with_logging=False)

Lets say there is a home page and a grid with rows on it. So, after clicking a row,
the grid disappears and the row is displayed with more detail. Something like this:

* Home page containing:

    - Grid Display

        + Rows

    - Show everything for one row

So on the Home page::

    from .. import global_var
    def __init__(self,**properties)
        global_var.publisher.subscribe(
            channel="one_row",
            subscriber=self,
            handler=self.selected)

    def selected(self, message):
        if message.title == "edit":
            print(message.content)

The, two levels down on the Rows page, there is this::

    from .. import global_var

    def link_row_click(self, **event_args):
        global_var.publisher.publish(channel='one_row',
            title='edit',
            content=self.item['id'])

And done. When the row is clicked (set its display with a link component),
the top form gets activated.

Nice!



