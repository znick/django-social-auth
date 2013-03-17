LinkedIn
========

LinkedIn setup is similar to any other OAuth service. To request extra fields
using `LinkedIn fields selectors`_ just define this setting::

    LINKEDIN_EXTRA_FIELD_SELECTORS = [...]

with the needed fields selectors, also define LINKEDIN_EXTRA_DATA properly as
described in `OAuth <oauth.html>`_, that way the values will be stored in
``UserSocialAuth.extra_data`` field.

By default ``id``, ``first-name`` and ``last-name`` are requested and stored.

If you want to request a user's email address, you'll need specify that your
application needs access to the email address using the ``r_emailaddress``
scope parameter. Also note that until they figure out a migration plan, they
require new API keys from the LinkedIn API (Issued after August 6th, 2012).

LinkedIn emulates the scope parameter of OAuth2 to specify user privileges.
Check here for `scope possibilities`_ if you need more than just the basic
profile.

These are declared as a list by defining this setting::

    LINKEDIN_SCOPE = ['r_basicprofile', ...]
    
For example, to request a user's email, headline, and industry from the
Linkedin API and store the information in ``UserSocialAuth.extra_data``, you
would add these settings::

    # Add email to requested authorizations.
    LINKEDIN_SCOPE = ['r_basicprofile', 'r_emailaddress', ...]
    # Add the fields so they will be requested from linkedin.
    LINKEDIN_EXTRA_FIELD_SELECTORS = ['email-address', 'headline', 'industry']
    # Arrange to add the fields to UserSocialAuth.extra_data
    LINKEDIN_EXTRA_DATA = [('id', 'id'),
                           ('first-name', 'first_name'),
                           ('last-name', 'last_name'),
                           ('email-address', 'email_address'),
                           ('headline', 'headline'),
                           ('industry', 'industry')]

.. _LinkedIn fields selectors: http://developer.linkedin.com/docs/DOC-1014
.. _scope possibilities: https://developer.linkedin.com/documents/authentication#granting
