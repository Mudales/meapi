.. image:: https://user-images.githubusercontent.com/42866208/164977163-2837836d-15bd-4a75-88fd-4e3fe2fd5dae.png
  :width: 95
  :alt: Me Logo
.. end-logo

`meapi <https://github.com/david-lev/meapi>`_: Unofficial api for 'Me - Caller ID & Spam Blocker'
##################################################################################################


.. image:: https://img.shields.io/pypi/dm/meapi?style=flat-square
    :alt: PyPI Downloads
    :target: https://pypi.org/project/meapi/

.. image:: https://badge.fury.io/py/meapi.svg
    :alt: PyPI Version
    :target: https://badge.fury.io/py/meapi

.. image:: https://www.codefactor.io/repository/github/david-lev/meapi/badge/main
   :target: https://www.codefactor.io/repository/github/david-lev/meapi/overview/main
   :alt: CodeFactor

.. image:: https://readthedocs.org/projects/meapi/badge/?version=latest&style=flat-square
   :target: https://meapi.readthedocs.io
   :alt: Docs

.. image:: https://badges.aleen42.com/src/telegram.svg
   :target: https://t.me/me_api
   :alt: Telegram

________________________

☎️ **meapi** is a Python3 library to identify, discover and get information about phone numbers, indicate and report spam, get and manage socials, profile management and much more.

🔐 To **get started**, read the `Setup guide <https://meapi.readthedocs.io/en/latest/content/setup.html>`_.

📖 For a **complete documentation** of available functions, see the `Reference <https://meapi.readthedocs.io/en/latest/content/reference.html>`_.

>>️ *For more information about Me® -* `Click here <https://meapp.co.il/>`_.


🎛 Installation
--------------
.. installation

- **Install using pip3:**

.. code-block:: bash

    pip3 install -U meapi

- **Install from source:**

.. code-block:: bash

    git clone https://github.com/mudales/meapi.git
    cd meapi && python3 setup.py install

.. end-installation

🎉 **Features**
---------------

🔎 Searching:
^^^^^^^^^^^^^

* 📞 Search phone numbers
* 😎 Get full user profile: profile picture, birthday, location, platform, socials and more
* 🚫 Spam indication and report

🌐 Social:
^^^^^^^^^^

* 📱 Get user social networks: facebook, instagram, twitter, spotify and more
* ✍️ See how people call you
* 🙌 Get mutual contacts
* 👁 See who watched your profile
* 🗑 See who deleted you from his contacts book
* 💬 Get, publish and manage comments
* 📍 Get users location
* 🔔 Read app notifications

⚙️ Settings:
^^^^^^^^^^^^^

* ✏ Change profile information
* 🛡 Configure social settings
* 🔗 Connect social networks (And get verified blue check)
* ⬆ Upload contacts and calls history
* ⛔ Block profiles and numbers
* ❌ Delete or suspend your account


👨‍💻 **Usage**
----------------
.. code-block:: python

    from meapi import Me

    # Initialize the client in interactive mode:
    me = Me(interactive_mode=True)

    # ☎ Get information about any phone number:
    res = me.phone_search('+972545416627')
    if res:
        print(res.name)

    # 😎 Get user full profile:
    if res.user:
        user = res.user
        print(f"{user.name=}, {user.email=}, {user.slogan=} {user.profile_picture=}")
        profile = res.get_profile()
        print(f"{profile.date_of_birth=}, {profile.location_name=}, {profile.gender=}, {profile.device_type=}")

        # 📱 Get social media accounts:
        for social in profile.social:
            if social:
                print(f"Social media ({social.name}): {social.profile_url}")
                for post in social.posts:
                    print(f"Post from {post.posted_at}:\n{post.text_first}\n{post.text_second}")

    # 💬 Watch, approve and like comments:
    for comment in me.get_comments():
        print(f"Comment from {comment.author.name}: {comment.message}")
        if comment.status == 'waiting':
            comment.approve()


    # ✍️ Change your profile details:
    my_profile = me.get_my_profile()
    my_profile.first_name = 'David'
    my_profile.last_name = 'Lev'

    # 🎴 Get your profile in vCard format:
    with open('/home/david/Downloads/my_vcard.vcf', 'w') as f:
        f.write(my_profile.as_vcard(dl_profile_picture=True))

    # 👥 See how people call you:
    for group in me.get_groups(sorted_by='count'):
        print(f"People named you '{group.name}' {group.count} times")

    # 👁 who watched your profile:
    for watcher in me.who_watched(incognito=True, sorted_by='last_view'):
        print(f"The user '{watcher.user.name}' watched you {watcher.count} times")

    # 🗑 who deleted you:
    for deleted in me.who_deleted():
        print(f"The user '{deleted.user.name}' deleted you at {deleted.created_at}")

    # ➕ And much much more...

📚 For more usage examples, read the `Examples <https://meapi.readthedocs.io/en/latest/content/examples.html>`_ page.

💾 **Requirements**
--------------------

- Python 3.6 or higher - https://www.python.org

📖 **Setup and Usage**
-----------------------

See the `Documentation <https://meapi.readthedocs.io/>`_ for detailed instructions

⛔ **Disclaimer**
------------------

**This application is intended for educational purposes only. Any use in professional manner or to harm anyone or any organization doesn't relate to me and can be considered as illegal.
Me name, its variations and the logo are registered trademarks of NFO LTD. I have nothing to do with the registered trademark.
I'm also not responsible for blocked accounts or any other damage caused by the use of this library. it is always
recommended to use virtual phone numbers for testing purposes.**

.. end-readme
