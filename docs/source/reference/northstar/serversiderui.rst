Serverside RUI
======

Server-side Rui provides a set of functions enabling servers to display complex hud elements on clients without requiring a client-side mod. These functions were introduced in Northstar ``1.10.0``.

It should be noted that there’s no guarantee the client will see the hud elements.

Polls
^^^^^

Creates a poll on ``player``.

.. figure:: /_static/serversiderui/vote.png
  :align: center
  :class: screenshot

  Player POV

**Definition:**

.. cpp:function:: void NSCreatePollOnPlayer( entity player, string header, array<string> options, float duration )

**Example:**

.. code-block:: javascript

    void function CreateDummyPoll()
     {
        array<string> options = [ "Me", "You", "Both of us" ]
        foreach(entity player in GetPlayerArray())
            NSCreatePollOnPlayer(player, "Vote who's the biggest dummy!", options, 30)
      }

Getting Response
-----

**Definition:**

.. cpp:function:: int NSGetPlayerResponse( entity player )

Returns the index of the item from ``options`` the player voted for. If the player hadn't voted yet it returns a -1.

**Example:**

.. code-block:: javascript

    void function CheckResponseToDummyPoll(entity player)
    {
        if(NSGetPlayerResponse(player) != -1)
            print("Player has voted!")
    }

Large Message
^^^^^

Sends a large message to ``player`` which will appear in the top right corner.

.. figure:: /_static/serversiderui/largemessage.gif
  :align: center
  :class: screenshot

  Player POV
  
**Definition:**

.. cpp:function:: void NSSendLargeMessageToPlayer( entity player, string title, string description, float duration, string image )

**Example:**

.. code-block:: javascript

    void function SendDummyLargeMessage(entity player)
    {
        NSSendLargeMessageToPlayer(player,"I'm not a dummy >:(", "You are", 10, "ui/fd_tutorial_tip.rpak")
    }

Info Message
^^^^^

Sends a smaller message to ``player`` which will appear from the center right.

.. figure:: /_static/serversiderui/info.gif
  :align: center
  :class: screenshot

  Player POV

**Definition:**

.. cpp:function:: void NSSendInfoMessageToPlayer( entity player, string text )

**Example:**

.. code-block:: javascript
  
    void function SendDummyInfoMessage(entity player)
    {
        NSSendInfoMessageToPlayer(player, "If you're reading this your a dummy")
    }

PopUp
^^^^^

Send a small popup to ``player`` which will appear in the lower half of their screen under their crosshair.

.. figure:: /_static/serversiderui/popup.gif
  :align: center
  :class: screenshot

  Player POV

**Definition:**

.. cpp:function:: void NSSendPopUpMessageToPlayer( entity player, string text )

**Example:**

.. code-block:: javascript

    void funcions SendDummyPopUp(entity player)
    {
        NSSendPopUpMessageToPlayer(player, "Dummy")
    }

Announcement
^^^^^

Sends a large announcement to ``player``.

.. figure:: /_static/serversiderui/announcement.gif
  :align: center
  :class: screenshot

  Player POV

**Definition:**

.. cpp:function:: void NSSendAnnouncementMessageToPlayer( entity player, string title, string description, vector color, int priority, int style )

**Example:**

.. code-block:: javascript

      void function SendDummyAnnouncement(entity player)
      {
          NSSendAnnouncementMessageToPlayer(player, "Large dummy", "Small dummy", <1,1,0>, 1, ANNOUNCEMENT_STYLE_QUICK)
      }

Status
^^^^^

Status messages allow you to show live data to the player.
Currently status messages are limited to 4 and there's no way to know if the player can see your message.

.. figure:: /_static/serversiderui/status.gif
   :align: center
   :class: screenshot

   Player POV

**Definitions:**

.. cpp:function:: void  NSCreateStatusMessageOnPlayer( entity player, string title, string description, string id )

Creates a status message on ``player``. ``id`` is used to identify and edit the message, make sure your id is unique!

.. cpp:function:: void  NSEditStatusMessageOnPlayer( entity player, string title, string description, string id  )

Allows for editing of the ``title`` and ``description`` of a message which was created using ``id``.

.. cpp:function:: void  NSDeleteStatusMessageOnPlayer( entity player, string id  )

Deletes the status message which was created with ``id``

**Examples:**

.. code-block:: javascript

    void function TestStatusMessage_Threaded(entity player)
    {
        string id = UniqueString("DUMMY_")
        NSCreateStatusMessageOnPlayer(player, "Dummies on server", "[0/1]", id)
        wait 3
        NSEditStatusMessageOnPlayer(player, "Dummies on server", "[1/1]", id)
        wait 10
        NSDeleteStatusMessageOnPlayer(player, id)    
    }