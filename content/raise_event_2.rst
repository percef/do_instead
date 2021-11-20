Programming on anvil.works
###########################
:tags: client
:category: anvil.works
:summary: Simple raise_event on child forms.
:date: 2021-11-20 6:53
:slug: raise-event-2

Custom Forms: Run Away!
==================================
Say you have a form with three smaller forms on it. **Do Not Make Those Forms "Custom"!**.
There will be so much pain if you do, not only in the present trying to understand
anvil.works' obtuse documentation on it (that could only be understood by the person who wrote it),
but also in the future when you will have to read that obtuse documentation again.

Instead
=======
Create the child form as you would normally create any form. On the child form's
user events::

  def text_box_1_pressed_enter(self, **event_args):
    """This method is called when the user presses Enter in this text box"""
    self.parent.raise_event(self.tag+"_box_1)

  def text_box_2_pressed_enter(self, **event_args):
    """This method is called when the user presses Enter in this text box"""
    self.parent.raise_event(self.tag+"_box_2)

In the parent form::

  def __init__(self,**properties):
    self.child_form.tag="child_A"
    self.add_event_handler(self.child_form.tag+"_box_1", self.text_1_handler)
    self.add_event_handler(self.child_form.tag+"_box_2", self.text_2_handler)

  self.text_1_handler(self,**event_args):
    # do stuff

  self.text_2_handler(self,**event_args):
    # do stuff

Nice!