:orphan:

Use Cases
=========

UserListGroups
--------------

.. code-block:: python

	>>> from groupy import Group
	>>> Group.list()
	>>> Group.list(former=True)

UserListMembers
---------------

.. code-block:: python

	>>> from groupy import Member, Group
	>>> Member.list()

UserListBots
------------

Currently: 

.. code-block:: python

	>>> from groupy import Bot
	>>> Bot.list()

UserCreateGroup
-----------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.create(name='name', )

UserUpdateGroup
---------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> group.update(name='name', ...)

UserDestroyGroup
----------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> group.destroy()
	>>> del group

*UserJoinGroup*
---------------

.. code-block:: python

	>>> from groupy import Group
	>>> Group.join(url='http://join_url')

UserJoinFormerGroup
-------------------

Currently: 

.. code-block:: python

	>>> from groupy import Group
	>>> former_group = Group.list(former=True)
	>>> former_group.add(User.get())

Eventually: 

.. code-block:: python

	>>> from groupy import Group
	>>> former_group = Group.list(former=True).first
	>>> group = former_group.join()

UserLeaveGroup
--------------

Currently: 

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> me = group.members.filter(user_id=User.get().user_id).first
	>>> group.remove(me)

Eventually: 

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> group.leave()

UserListGroupMessages
---------------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> group.messages()
	>>> group.messages(after=123456789)
	>>> group.messages(before=123456789)
	>>> group.messages(since=123456789)

UserListMemberMessages
----------------------

.. code-block:: python

	>>> from groupy import Member
	>>> member = Member.list().first
	>>> member.messages()
	>>> member.messages(after=123456789)
	>>> member.messages(before=123456789)
	>>> member.messages(since=123456789)

UserAddGroupMember
------------------

.. code-block:: python

	>>> from groupy import Group, Member
	>>> member, *members = Member.list()
	>>> group = Group.list().first
	>>> group.add(member)
	>>> group.add(*members)

UserRemoveGroupMember
---------------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> member, *members = group.members()
	>>> group.remove(member)
	>>> for m in members:
	...     group.remove(m)
	... 

*UserCheckMemberAddResults*
---------------------------

``pass`` :-)


UserPostGroupMessage
--------------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> group.post("Hello")

UserPostMemberMessage
---------------------

.. code-block:: python

	>>> from groupy import Member
	>>> member = Member.list().first
	>>> member.post("Hello")

UserLikeMessage
---------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> message = group.messages().newest
	>>> message.like()

UserUnlikeMessage
-----------------

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> message = group.messages().newest
	>>> message.unlike()

UserGetUser
-----------

.. code-block:: python

	>>> from groupy import User
	>>> me = User.get()

UserEnableSms
-------------

.. code-block:: python

	>>> from groupy import User
	>>> User.enable_sms(duration=4, registration_token='TOKEN')

UserDisableSms
--------------

.. code-block:: python

	>>> from groupy import User
	>>> User.disable_sms()

UserCreateBot
-------------

Currently: 

.. code-block:: python

	>>> from groupy import Bot, Group
	>>> group = Group.list().first
	>>> bot = Bot.create(name='name', group)

Eventually: 

.. code-block:: python

	>>> from groupy import Group
	>>> group = Group.list().first
	>>> bot = group.create_bot(name='name')

UserUpdateBot
-------------

.. code-block:: python

	>>> from groupy import Bot
	>>> bot = Bot.list().first
	>>> bot.update(name='name', ...)

UserDestroyBot
--------------

.. code-block:: python

	>>> from groupy import Bot
	>>> bot = Bot.list().first
	>>> bot.destroy()
	>>> del bot

BotPostMessage
--------------

.. code-block:: python

	>>> from groupy import Bot
	>>> bot = Bot.list().first
	>>> bot.post("Hello")


Advanced Usage
==============

- Retreive messages based on time
- Working with lists
	+ Filter lists
	+ Messsage pagers
- Creating attachments
	+ Images
	+ Locations
	+ Emoji
- When it just doesn't work out...
	+ Leaving a group
	+ Disbanding (destroying) a group you own
	+ Destroying a bot
- The SMS mode
	+ Enabling and you
	+ Disabling
