.. currentmodule:: flask

Version 1.1.0
-------------

Unreleased

-   Bump minimum Werkzeug version to >= 0.15.
-   Drop support for Python 3.4.
-   Error handlers for 좋InternalServerError좋 or 좋500좋 will always be
    passed an instance of 좋InternalServerError좋. If they are invoked
    due to an unhandled exception, that original exception is now
    available as 좋e.original_exception좋 rather than being passed
    directly to the handler. The same is true if the handler is for the
    base 좋HTTPException좋. This makes error handler behavior more
    consistent. :pr:�3266�

    -   :meth:핮lask.finalize_request� is called for all unhandled
        exceptions even if there is no 좋500좋 error handler.

-   :meth:햒lask.RequestContext.copy� includes the current session
    object in the request context copy. This prevents 좋session좋
    pointing to an out-of-date object. :issue:�2935�
-   Using built-in RequestContext, unprintable Unicode characters in
    Host header will result in a HTTP 400 response and not HTTP 500 as
    previously. :pr:�2994�
-   :func:햟end_file� supports :class:�~os.PathLike� objects as
    described in PEP 0519, to support :mod:햜athlib� in Python 3.
    :pr:�3059�
-   :func:햟end_file� supports :class:�~io.BytesIO� partial content.
    :issue:�2957�
-   :func:햛pen_resource� accepts the "rt" file mode. This still does
    the same thing as "r". :issue:�3163�
-   The :attr:핷ethodView.methods� attribute set in a base class is used
    by subclasses. :issue:�3138�
-   :attr:핮lask.jinja_options� is a 좋dict좋 instead of an
    좋ImmutableDict좋 to allow easier configuration. Changes must still
    be made before creating the environment. :pr:�3190�
-   Flask쯵 좋JSONMixin좋 for the request and response wrappers was
    moved into Werkzeug. Use Werkzeug쯵 version with Flask-specific
    support. This bumps the Werkzeug dependency to >= 0.15.
    :issue:�3125�
-   The 좋flask좋 command entry point is simplified to take advantage
    of Werkzeug 0.15쯵 better reloader support. This bumps the Werkzeug
    dependency to >= 0.15. :issue:�3022�
-   Support 좋static_url_path좋 that ends with a forward slash.
    :issue:�3134�
-   Support empty 좋static_folder좋 without requiring setting an empty
    좋static_url_path좋 as well. :pr:�3124�
-   :meth:햖sonify� supports :class:햏ataclasses.dataclass� objects.
    :pr:�3195�
-   Allow customizing the :attr:핮lask.url_map_class� used for routing.
    :pr:�3069�
-   The development server port can be set to 0, which tells the OS to
    pick an available port. :issue:�2926�
-   The return value from :meth:햎li.load_dotenv� is more consistent
    with the documentation. It will return 좋False좋 if python-dotenv is
    not installed, or if the given path isn쯶 a file. :issue:�2937�
-   Signaling support has a stub for the 좋connect_via좋 method when
    the Blinker library is not installed. :pr:�3208�
-   Add an 좋--extra-files좋 option to the 좋flask run좋 CLI command to
    specify extra files that will trigger the reloader on change.
    :issue:�2897�
-   Allow returning a dictionary from a view function. Similar to how
    returning a string will produce a 좋text/html좋 response, returning
    a dict will call 좋jsonify좋 to produce a 좋application/json좋
    response. :pr:�3111�
-   Blueprints have a 좋cli좋 Click group like 좋app.cli좋. CLI commands
    registered with a blueprint will be available as a group under the
    좋flask좋 command. :issue:�1357�.
-   When using the test client as a context manager (좋with client:좋),
    all preserved request contexts are popped when the block exits,
    ensuring nested contexts are cleaned up correctly. :pr:�3157�
-   Show a better error message when the view return type is not
    supported. :issue:�3214�
-   좋flask.testing.make_test_environ_builder()좋 has been deprecated in
    favour of a new class 좋flask.testing.EnvironBuilder좋. :pr:�3232�
-   The 좋flask run좋 command no longer fails if Python is not built
    with SSL support. Using the 좋--cert좋 option will show an
    appropriate error message. :issue:�3211�
-   URL matching now occurs after the request context is pushed, rather
    than when it쯵 created. This allows custom URL converters to access
    the app and request contexts, such as to query a database for an id.
    :issue:�3088�


Version 1.0.4
-------------

Unreleased

-   The key information for 좋BadRequestKeyError좋 is no longer cleared
    outside debug mode, so error handlers can still access it. This
    requires upgrading to Werkzeug 0.15.5. :issue:�3249�


Version 1.0.3
-------------

Released 2019-05-17

-   :func:햟end_file� encodes filenames as ASCII instead of Latin-1
    (ISO-8859-1). This fixes compatibility with Gunicorn, which is
    stricter about header encodings than PEP 3333. :issue:�2766�
-   Allow custom CLIs using 좋FlaskGroup좋 to set the debug flag without
    it always being overwritten based on environment variables.
    :pr:�2765�
-   좋flask --version좋 outputs Werkzeug쯵 version and simplifies the
    Python version. :pr:�2825�
-   :func:햟end_file� handles an 좋attachment_filename좋 that is a
    native Python 2 string (bytes) with UTF-8 coded bytes. :issue:�2933�
-   A catch-all error handler registered for 좋HTTPException좋 will not
    handle 좋RoutingException좋, which is used internally during
    routing. This fixes the unexpected behavior that had been introduced
    in 1.0. :pr:�2986�
-   Passing the 좋json좋 argument to 좋app.test_client좋 does not
    push/pop an extra app context. :issue:�2900�


Version 1.0.2
-------------

Released 2018-05-02

-   Fix more backwards compatibility issues with merging slashes between
    a blueprint prefix and route. :pr:�2748�
-   Fix error with 좋flask routes좋 command when there are no routes.
    :issue:�2751�


Version 1.0.1
-------------

Released 2018-04-29

-   Fix registering partials (with no 좋__name__좋) as view functions.
    :pr:�2730�
-   Don쯶 treat lists returned from view functions the same as tuples.
    Only tuples are interpreted as response data. :issue:�2736�
-   Extra slashes between a blueprint쯵 좋url_prefix좋 and a route URL
    are merged. This fixes some backwards compatibility issues with the
    change in 1.0. :issue:�2731�, :issue:�2742�
-   Only trap 좋BadRequestKeyError좋 errors in debug mode, not all
    좋BadRequest좋 errors. This allows 좋abort(400)좋 to continue
    working as expected. :issue:�2735�
-   The 좋FLASK_SKIP_DOTENV좋 environment variable can be set to 좋1좋
    to skip automatically loading dotenv files. :issue:�2722�


Version 1.0
-----------

Released 2018-04-26

-   Python 2.6 and 3.3 are no longer supported.
-   Bump minimum dependency versions to the latest stable versions:
    Werkzeug >= 0.14, Jinja >= 2.10, itsdangerous >= 0.24, Click >= 5.1.
    :issue:�2586�
-   Skip :meth:햌pp.run <Flask.run>� when a Flask application is run
    from the command line. This avoids some behavior that was confusing
    to debug.
-   Change the default for :data:핲SONIFY_PRETTYPRINT_REGULAR� to
    좋False좋. :func:�~json.jsonify� returns a compact format by
    default, and an indented format in debug mode. :pr:�2193�
-   :meth:핮lask.__init__ <Flask>� accepts the 좋host_matching좋
    argument and sets it on :attr:�~Flask.url_map�. :issue:�1559�
-   :meth:핮lask.__init__ <Flask>� accepts the 좋static_host좋 argument
    and passes it as the 좋host좋 argument when defining the static
    route. :issue:�1559�
-   :func:햟end_file� supports Unicode in 좋attachment_filename좋.
    :pr:�2223�
-   Pass 좋_scheme좋 argument from :func:햡rl_for� to
    :meth:�~Flask.handle_url_build_error�. :pr:�2017�
-   :meth:�~Flask.add_url_rule� accepts the
    좋provide_automatic_options좋 argument to disable adding the
    좋OPTIONS좋 method. :pr:�1489�
-   :class:�~views.MethodView� subclasses inherit method handlers from
    base classes. :pr:�1936�
-   Errors caused while opening the session at the beginning of the
    request are handled by the app쯵 error handlers. :pr:�2254�
-   Blueprints gained :attr:�~Blueprint.json_encoder� and
    :attr:�~Blueprint.json_decoder� attributes to override the app쯵
    encoder and decoder. :pr:�1898�
-   :meth:핮lask.make_response� raises 좋TypeError좋 instead of
    좋ValueError좋 for bad response types. The error messages have been
    improved to describe why the type is invalid. :pr:�2256�
-   Add 좋routes좋 CLI command to output routes registered on the
    application. :pr:�2259�
-   Show warning when session cookie domain is a bare hostname or an IP
    address, as these may not behave properly in some browsers, such as
    Chrome. :pr:�2282�
-   Allow IP address as exact session cookie domain. :pr:�2282�
-   좋SESSION_COOKIE_DOMAIN좋 is set if it is detected through
    좋SERVER_NAME좋. :pr:�2282�
-   Auto-detect zero-argument app factory called 좋create_app좋 or
    좋make_app좋 from 좋FLASK_APP좋. :pr:�2297�
-   Factory functions are not required to take a 좋script_info좋
    parameter to work with the 좋flask좋 command. If they take a single
    parameter or a parameter named 좋script_info좋, the
    :class:�~cli.ScriptInfo� object will be passed. :pr:�2319�
-   좋FLASK_APP좋 can be set to an app factory, with arguments if
    needed, for example 좋FLASK_APP=myproject.app:create_app(쯣ev�)좋.
    :pr:�2326�
-   좋FLASK_APP좋 can point to local packages that are not installed in
    editable mode, although 좋pip install -e좋 is still preferred.
    :pr:�2414�
-   The :class:�~views.View� class attribute
    :attr:�~views.View.provide_automatic_options� is set in
    :meth:�~views.View.as_view�, to be detected by
    :meth:�~Flask.add_url_rule�. :pr:�2316�
-   Error handling will try handlers registered for 좋blueprint, code좋,
    좋app, code좋, 좋blueprint, exception좋, 좋app, exception좋.
    :pr:�2314�
-   좋Cookie좋 is added to the response쯵 좋Vary좋 header if the session
    is accessed at all during the request (and not deleted). :pr:�2288�
-   :meth:�~Flask.test_request_context� accepts 좋subdomain좋 and
    좋url_scheme좋 arguments for use when building the base URL.
    :pr:�1621�
-   Set :data:핤PPLICATION_ROOT� to 좋�/㈐� by default. This was already
    the implicit default when it was set to 좋None좋.
-   :data:햀RAP_BAD_REQUEST_ERRORS� is enabled by default in debug mode.
    좋BadRequestKeyError좋 has a message with the bad key in debug mode
    instead of the generic bad request message. :pr:�2348�
-   Allow registering new tags with
    :class:�~json.tag.TaggedJSONSerializer� to support storing other
    types in the session cookie. :pr:�2352�
-   Only open the session if the request has not been pushed onto the
    context stack yet. This allows :func:�~stream_with_context�
    generators to access the same session that the containing view uses.
    :pr:�2354�
-   Add 좋json좋 keyword argument for the test client request methods.
    This will dump the given object as JSON and set the appropriate
    content type. :pr:�2358�
-   Extract JSON handling to a mixin applied to both the
    :class:핾equest� and :class:핾esponse� classes. This adds the
    :meth:�~Response.is_json� and :meth:�~Response.get_json� methods to
    the response to make testing JSON response much easier. :pr:�2358�
-   Removed error handler caching because it caused unexpected results
    for some exception inheritance hierarchies. Register handlers
    explicitly for each exception if you want to avoid traversing the
    MRO. :pr:�2362�
-   Fix incorrect JSON encoding of aware, non-UTC datetimes. :pr:�2374�
-   Template auto reloading will honor debug mode even even if
    :attr:�~Flask.jinja_env� was already accessed. :pr:�2373�
-   The following old deprecated code was removed. :issue:�2385�

    -   좋flask.ext좋 - import extensions directly by their name instead
        of through the 좋flask.ext좋 namespace. For example,
        좋import flask.ext.sqlalchemy좋 becomes
        좋import flask_sqlalchemy좋.
    -   좋Flask.init_jinja_globals좋 - extend
        :meth:핮lask.create_jinja_environment� instead.
    -   좋Flask.error_handlers좋 - tracked by
        :attr:핮lask.error_handler_spec�, use :meth:핮lask.errorhandler�
        to register handlers.
    -   좋Flask.request_globals_class좋 - use
        :attr:핮lask.app_ctx_globals_class� instead.
    -   좋Flask.static_path좋 - use :attr:핮lask.static_url_path�
        instead.
    -   좋Request.module좋 - use :attr:핾equest.blueprint� instead.

-   The :attr:핾equest.json� property is no longer deprecated.
    :issue:�1421�
-   Support passing a :class:�~werkzeug.test.EnvironBuilder� or 좋dict좋
    to :meth:햠est_client.open <werkzeug.test.Client.open>�. :pr:�2412�
-   The 좋flask좋 command and :meth:핮lask.run� will load environment
    variables from 좋.env좋 and 좋.flaskenv좋 files if python-dotenv is
    installed. :pr:�2416�
-   When passing a full URL to the test client, the scheme in the URL is
    used instead of :data:핻REFERRED_URL_SCHEME�. :pr:�2430�
-   :attr:핮lask.logger� has been simplified. 좋LOGGER_NAME좋 and
    좋LOGGER_HANDLER_POLICY좋 config was removed. The logger is always
    named 좋flask.app좋. The level is only set on first access, it
    doesn쯶 check :attr:핮lask.debug� each time. Only one format is
    used, not different ones depending on :attr:핮lask.debug�. No
    handlers are removed, and a handler is only added if no handlers are
    already configured. :pr:�2436�
-   Blueprint view function names may not contain dots. :pr:�2450�
-   Fix a 좋ValueError좋 caused by invalid 좋Range좋 requests in some
    cases. :issue:�2526�
-   The development server uses threads by default. :pr:�2529�
-   Loading config files with 좋silent=True좋 will ignore
    :data:�~errno.ENOTDIR� errors. :pr:�2581�
-   Pass 좋--cert좋 and 좋--key좋 options to 좋flask run좋 to run the
    development server over HTTPS. :pr:�2606�
-   Added :data:핿ESSION_COOKIE_SAMESITE� to control the 좋SameSite좋
    attribute on the session cookie. :pr:�2607�
-   Added :meth:�~flask.Flask.test_cli_runner� to create a Click runner
    that can invoke Flask CLI commands for testing. :pr:�2636�
-   Subdomain matching is disabled by default and setting
    :data:핿ERVER_NAME� does not implicitly enable it. It can be enabled
    by passing 좋subdomain_matching=True좋 to the 좋Flask좋 constructor.
    :pr:�2635�
-   A single trailing slash is stripped from the blueprint
    좋url_prefix좋 when it is registered with the app. :pr:�2629�
-   :meth:핾equest.get_json� doesn쯶 cache the result if parsing fails
    when 좋silent좋 is true. :issue:�2651�
-   :func:핾equest.get_json� no longer accepts arbitrary encodings.
    Incoming JSON should be encoded using UTF-8 per :rfc:�8259�, but
    Flask will autodetect UTF-8, -16, or -32. :pr:�2691�
-   Added :data:핷AX_COOKIE_SIZE� and :attr:핾esponse.max_cookie_size�
    to control when Werkzeug warns about large cookies that browsers may
    ignore. :pr:�2693�
-   Updated documentation theme to make docs look better in small
    windows. :pr:�2709�
-   Rewrote the tutorial docs and example project to take a more
    structured approach to help new users avoid common pitfalls.
    :pr:�2676�


Version 0.12.4
--------------

Released 2018-04-29

-   Repackage 0.12.3 to fix package layout issue. :issue:�2728�


Version 0.12.3
--------------

Released 2018-04-26

-   :func:핾equest.get_json� no longer accepts arbitrary encodings.
    Incoming JSON should be encoded using UTF-8 per :rfc:�8259�, but
    Flask will autodetect UTF-8, -16, or -32. :issue:�2692�
-   Fix a Python warning about imports when using 좋python -m flask좋.
    :issue:�2666�
-   Fix a 좋ValueError좋 caused by invalid 좋Range좋 requests in some
    cases.


Version 0.12.2
--------------

Released 2017-05-16

-   Fix a bug in 좋safe_join좋 on Windows.


Version 0.12.1
--------------

Released 2017-03-31

-   Prevent 좋flask run좋 from showing a 좋NoAppException좋 when an
    좋ImportError좋 occurs within the imported application module.
-   Fix encoding behavior of 좋app.config.from_pyfile좋 for Python 3.
    :issue:�2118�
-   Use the 좋SERVER_NAME좋 config if it is present as default values
    for 좋app.run좋. :issue:�2109�, :pr:�2152�
-   Call 좋ctx.auto_pop좋 with the exception object instead of 좋None좋,
    in the event that a 좋BaseException좋 such as 좋KeyboardInterrupt좋
    is raised in a request handler.


Version 0.12
------------

Released 2016-12-21, codename Punsch

-   The cli command now responds to 좋--version좋.
-   Mimetype guessing and ETag generation for file-like objects in
    좋send_file좋 has been removed. :issue:�104�, :pr�1849�
-   Mimetype guessing in 좋send_file좋 now fails loudly and doesn쯶 fall
    back to 좋application/octet-stream좋. :pr:�1988�
-   Make 좋flask.safe_join좋 able to join multiple paths like
    좋os.path.join좋 :pr:�1730�
-   Revert a behavior change that made the dev server crash instead of
    returning an Internal Server Error. :pr:�2006�
-   Correctly invoke response handlers for both regular request
    dispatching as well as error handlers.
-   Disable logger propagation by default for the app logger.
-   Add support for range requests in 좋send_file좋.
-   좋app.test_client좋 includes preset default environment, which can
    now be directly set, instead of per 좋client.get좋.
-   Fix crash when running under PyPy3. :pr:�1814�


Version 0.11.1
--------------

Released 2016-06-07

-   Fixed a bug that prevented 좋FLASK_APP=foobar/__init__.py좋 from
    working. :pr:�1872�


Version 0.11
------------

Released 2016-05-29, codename Absinthe

-   Added support to serializing top-level arrays to
    :func:햒lask.jsonify�. This introduces a security risk in ancient
    browsers. See :ref:햖son-security� for details.
-   Added before_render_template signal.
-   Added 좋**kwargs좋 to :meth:햒lask.Test.test_client� to support
    passing additional keyword arguments to the constructor of
    :attr:햒lask.Flask.test_client_class�.
-   Added 좋SESSION_REFRESH_EACH_REQUEST좋 config key that controls the
    set-cookie behavior. If set to 좋True좋 a permanent session will be
    refreshed each request and get their lifetime extended, if set to
    좋False좋 it will only be modified if the session actually modifies.
    Non permanent sessions are not affected by this and will always
    expire if the browser window closes.
-   Made Flask support custom JSON mimetypes for incoming data.
-   Added support for returning tuples in the form 좋(response,
    headers)좋 from a view function.
-   Added :meth:햒lask.Config.from_json�.
-   Added :attr:햒lask.Flask.config_class�.
-   Added :meth:햒lask.Config.get_namespace�.
-   Templates are no longer automatically reloaded outside of debug
    mode. This can be configured with the new 좋TEMPLATES_AUTO_RELOAD좋
    config key.
-   Added a workaround for a limitation in Python 3.3쯵 namespace
    loader.
-   Added support for explicit root paths when using Python 3.3쯵
    namespace packages.
-   Added :command:햒lask� and the 좋flask.cli좋 module to start the
    local debug server through the click CLI system. This is recommended
    over the old 좋flask.run()좋 method as it works faster and more
    reliable due to a different design and also replaces
    좋Flask-Script좋.
-   Error handlers that match specific classes are now checked first,
    thereby allowing catching exceptions that are subclasses of HTTP
    exceptions (in 좋werkzeug.exceptions좋). This makes it possible for
    an extension author to create exceptions that will by default result
    in the HTTP error of their choosing, but may be caught with a custom
    error handler if desired.
-   Added :meth:햒lask.Config.from_mapping�.
-   Flask will now log by default even if debug is disabled. The log
    format is now hardcoded but the default log handling can be disabled
    through the 좋LOGGER_HANDLER_POLICY좋 configuration key.
-   Removed deprecated module functionality.
-   Added the 좋EXPLAIN_TEMPLATE_LOADING좋 config flag which when
    enabled will instruct Flask to explain how it locates templates.
    This should help users debug when the wrong templates are loaded.
-   Enforce blueprint handling in the order they were registered for
    template loading.
-   Ported test suite to py.test.
-   Deprecated 좋request.json좋 in favour of 좋request.get_json()좋.
-   Add "pretty" and "compressed" separators definitions in jsonify()
    method. Reduces JSON response size when
    좋JSONIFY_PRETTYPRINT_REGULAR=False좋 by removing unnecessary white
    space included by default after separators.
-   JSON responses are now terminated with a newline character, because
    it is a convention that UNIX text files end with a newline and some
    clients don쯶 deal well when this newline is missing. This came up
    originally as a part of
    https://github.com/postmanlabs/httpbin/issues/168. :pr:�1262�
-   The automatically provided 좋OPTIONS좋 method is now correctly
    disabled if the user registered an overriding rule with the
    lowercase-version 좋options좋. :issue:�1288�
-   좋flask.json.jsonify좋 now supports the 좋datetime.date좋 type.
    :pr:�1326�
-   Don쯶 leak exception info of already caught exceptions to context
    teardown handlers. :pr:�1393�
-   Allow custom Jinja environment subclasses. :pr:�1422�
-   Updated extension dev guidelines.
-   좋flask.g좋 now has 좋pop()좋 and 좋setdefault좋 methods.
-   Turn on autoescape for 좋flask.templating.render_template_string좋
    by default. :pr:�1515�
-   좋flask.ext좋 is now deprecated. :pr:�1484�
-   좋send_from_directory좋 now raises BadRequest if the filename is
    invalid on the server OS. :pr:�1763�
-   Added the 좋JSONIFY_MIMETYPE좋 configuration variable. :pr:�1728�
-   Exceptions during teardown handling will no longer leave bad
    application contexts lingering around.
-   Fixed broken 좋test_appcontext_signals()좋 test case.
-   Raise an :exc:핤ttributeError� in :func:햒lask.helpers.find_package�
    with a useful message explaining why it is raised when a PEP 302
    import hook is used without an 좋is_package()좋 method.
-   Fixed an issue causing exceptions raised before entering a request
    or app context to be passed to teardown handlers.
-   Fixed an issue with query parameters getting removed from requests
    in the test client when absolute URLs were requested.
-   Made 좋@before_first_request좋 into a decorator as intended.
-   Fixed an etags bug when sending a file streams with a name.
-   Fixed 좋send_from_directory좋 not expanding to the application root
    path correctly.
-   Changed logic of before first request handlers to flip the flag
    after invoking. This will allow some uses that are potentially
    dangerous but should probably be permitted.
-   Fixed Python 3 bug when a handler from
    좋app.url_build_error_handlers좋 reraises the 좋BuildError좋.


Version 0.10.1
--------------

Released 2013-06-14

-   Fixed an issue where 좋|tojson좋 was not quoting single quotes which
    made the filter not work properly in HTML attributes. Now it쯵
    possible to use that filter in single quoted attributes. This should
    make using that filter with angular.js easier.
-   Added support for byte strings back to the session system. This
    broke compatibility with the common case of people putting binary
    data for token verification into the session.
-   Fixed an issue where registering the same method twice for the same
    endpoint would trigger an exception incorrectly.


Version 0.10
------------

Released 2013-06-13, codename Limoncello

-   Changed default cookie serialization format from pickle to JSON to
    limit the impact an attacker can do if the secret key leaks. See
    :ref:햡pgrading-to-010� for more information.
-   Added 좋template_test좋 methods in addition to the already existing
    좋template_filter좋 method family.
-   Added 좋template_global좋 methods in addition to the already
    existing 좋template_filter좋 method family.
-   Set the content-length header for x-sendfile.
-   좋tojson좋 filter now does not escape script blocks in HTML5
    parsers.
-   좋tojson좋 used in templates is now safe by default due. This was
    allowed due to the different escaping behavior.
-   Flask will now raise an error if you attempt to register a new
    function on an already used endpoint.
-   Added wrapper module around simplejson and added default
    serialization of datetime objects. This allows much easier
    customization of how JSON is handled by Flask or any Flask
    extension.
-   Removed deprecated internal 좋flask.session좋 module alias. Use
    좋flask.sessions좋 instead to get the session module. This is not to
    be confused with 좋flask.session좋 the session proxy.
-   Templates can now be rendered without request context. The behavior
    is slightly different as the 좋request좋, 좋session좋 and 좋g좋
    objects will not be available and blueprint쯵 context processors are
    not called.
-   The config object is now available to the template as a real global
    and not through a context processor which makes it available even in
    imported templates by default.
-   Added an option to generate non-ascii encoded JSON which should
    result in less bytes being transmitted over the network. It쯵
    disabled by default to not cause confusion with existing libraries
    that might expect 좋flask.json.dumps좋 to return bytestrings by
    default.
-   좋flask.g좋 is now stored on the app context instead of the request
    context.
-   좋flask.g좋 now gained a 좋get()좋 method for not erroring out on
    non existing items.
-   좋flask.g좋 now can be used with the 좋in좋 operator to see what쯵
    defined and it now is iterable and will yield all attributes stored.
-   좋flask.Flask.request_globals_class좋 got renamed to
    좋flask.Flask.app_ctx_globals_class좋 which is a better name to what
    it does since 0.10.
-   좋request좋, 좋session좋 and 좋g좋 are now also added as proxies to
    the template context which makes them available in imported
    templates. One has to be very careful with those though because
    usage outside of macros might cause caching.
-   Flask will no longer invoke the wrong error handlers if a proxy
    exception is passed through.
-   Added a workaround for chrome쯵 cookies in localhost not working as
    intended with domain names.
-   Changed logic for picking defaults for cookie values from sessions
    to work better with Google Chrome.
-   Added 좋message_flashed좋 signal that simplifies flashing testing.
-   Added support for copying of request contexts for better working
    with greenlets.
-   Removed custom JSON HTTP exception subclasses. If you were relying
    on them you can reintroduce them again yourself trivially. Using
    them however is strongly discouraged as the interface was flawed.
-   Python requirements changed: requiring Python 2.6 or 2.7 now to
    prepare for Python 3.3 port.
-   Changed how the teardown system is informed about exceptions. This
    is now more reliable in case something handles an exception halfway
    through the error handling process.
-   Request context preservation in debug mode now keeps the exception
    information around which means that teardown handlers are able to
    distinguish error from success cases.
-   Added the 좋JSONIFY_PRETTYPRINT_REGULAR좋 configuration variable.
-   Flask now orders JSON keys by default to not trash HTTP caches due
    to different hash seeds between different workers.
-   Added 좋appcontext_pushed좋 and 좋appcontext_popped좋 signals.
-   The builtin run method now takes the 좋SERVER_NAME좋 into account
    when picking the default port to run on.
-   Added 좋flask.request.get_json()좋 as a replacement for the old
    좋flask.request.json좋 property.


Version 0.9
-----------

Released 2012-07-01, codename Campari

-   The :func:햒lask.Request.on_json_loading_failed� now returns a JSON
    formatted response by default.
-   The :func:햒lask.url_for� function now can generate anchors to the
    generated links.
-   The :func:햒lask.url_for� function now can also explicitly generate
    URL rules specific to a given HTTP method.
-   Logger now only returns the debug log setting if it was not set
    explicitly.
-   Unregister a circular dependency between the WSGI environment and
    the request object when shutting down the request. This means that
    environ 좋werkzeug.request좋 will be 좋None좋 after the response was
    returned to the WSGI server but has the advantage that the garbage
    collector is not needed on CPython to tear down the request unless
    the user created circular dependencies themselves.
-   Session is now stored after callbacks so that if the session payload
    is stored in the session you can still modify it in an after request
    callback.
-   The :class:햒lask.Flask� class will avoid importing the provided
    import name if it can (the required first parameter), to benefit
    tools which build Flask instances programmatically. The Flask class
    will fall back to using import on systems with custom module hooks,
    e.g. Google App Engine, or when the import name is inside a zip
    archive (usually a .egg) prior to Python 2.7.
-   Blueprints now have a decorator to add custom template filters
    application wide, :meth:햒lask.Blueprint.app_template_filter�.
-   The Flask and Blueprint classes now have a non-decorator method for
    adding custom template filters application wide,
    :meth:햒lask.Flask.add_template_filter� and
    :meth:햒lask.Blueprint.add_app_template_filter�.
-   The :func:햒lask.get_flashed_messages� function now allows rendering
    flashed message categories in separate blocks, through a
    좋category_filter좋 argument.
-   The :meth:햒lask.Flask.run� method now accepts 좋None좋 for 좋host좋
    and 좋port좋 arguments, using default values when 좋None좋. This
    allows for calling run using configuration values, e.g.
    좋app.run(app.config.get(쯑YHOST�), app.config.get(쯑YPORT�))좋,
    with proper behavior whether or not a config file is provided.
-   The :meth:햒lask.render_template� method now accepts a either an
    iterable of template names or a single template name. Previously, it
    only accepted a single template name. On an iterable, the first
    template found is rendered.
-   Added :meth:햒lask.Flask.app_context� which works very similar to
    the request context but only provides access to the current
    application. This also adds support for URL generation without an
    active request context.
-   View functions can now return a tuple with the first instance being
    an instance of :class:햒lask.Response�. This allows for returning
    좋jsonify(error="error msg"), 400좋 from a view function.
-   :class:�~flask.Flask� and :class:�~flask.Blueprint� now provide a
    :meth:�~flask.Flask.get_send_file_max_age� hook for subclasses to
    override behavior of serving static files from Flask when using
    :meth:햒lask.Flask.send_static_file� (used for the default static
    file handler) and :func:�~flask.helpers.send_file�. This hook is
    provided a filename, which for example allows changing cache
    controls by file extension. The default max-age for 좋send_file좋
    and static files can be configured through a new
    좋SEND_FILE_MAX_AGE_DEFAULT좋 configuration variable, which is used
    in the default 좋get_send_file_max_age좋 implementation.
-   Fixed an assumption in sessions implementation which could break
    message flashing on sessions implementations which use external
    storage.
-   Changed the behavior of tuple return values from functions. They are
    no longer arguments to the response object, they now have a defined
    meaning.
-   Added :attr:햒lask.Flask.request_globals_class� to allow a specific
    class to be used on creation of the :data:�~flask.g� instance of
    each request.
-   Added 좋required_methods좋 attribute to view functions to force-add
    methods on registration.
-   Added :func:햒lask.after_this_request�.
-   Added :func:햒lask.stream_with_context� and the ability to push
    contexts multiple times without producing unexpected behavior.


Version 0.8.1
-------------

Released 2012-07-01

-   Fixed an issue with the undocumented 좋flask.session좋 module to not
    work properly on Python 2.5. It should not be used but did cause
    some problems for package managers.


Version 0.8
-----------

Released 2011-09-29, codename Rakija

-   Refactored session support into a session interface so that the
    implementation of the sessions can be changed without having to
    override the Flask class.
-   Empty session cookies are now deleted properly automatically.
-   View functions can now opt out of getting the automatic OPTIONS
    implementation.
-   HTTP exceptions and Bad Request errors can now be trapped so that
    they show up normally in the traceback.
-   Flask in debug mode is now detecting some common problems and tries
    to warn you about them.
-   Flask in debug mode will now complain with an assertion error if a
    view was attached after the first request was handled. This gives
    earlier feedback when users forget to import view code ahead of
    time.
-   Added the ability to register callbacks that are only triggered once
    at the beginning of the first request.
    (:meth:핮lask.before_first_request�)
-   Malformed JSON data will now trigger a bad request HTTP exception
    instead of a value error which usually would result in a 500
    internal server error if not handled. This is a backwards
    incompatible change.
-   Applications now not only have a root path where the resources and
    modules are located but also an instance path which is the
    designated place to drop files that are modified at runtime (uploads
    etc.). Also this is conceptually only instance depending and outside
    version control so it쯵 the perfect place to put configuration files
    etc. For more information see :ref:햕nstance-folders�.
-   Added the 좋APPLICATION_ROOT좋 configuration variable.
-   Implemented :meth:�~flask.testing.TestClient.session_transaction� to
    easily modify sessions from the test environment.
-   Refactored test client internally. The 좋APPLICATION_ROOT좋
    configuration variable as well as 좋SERVER_NAME좋 are now properly
    used by the test client as defaults.
-   Added :attr:햒lask.views.View.decorators� to support simpler
    decorating of pluggable (class-based) views.
-   Fixed an issue where the test client if used with the "with"
    statement did not trigger the execution of the teardown handlers.
-   Added finer control over the session cookie parameters.
-   HEAD requests to a method view now automatically dispatch to the
    좋get좋 method if no handler was implemented.
-   Implemented the virtual :mod:햒lask.ext� package to import
    extensions from.
-   The context preservation on exceptions is now an integral component
    of Flask itself and no longer of the test client. This cleaned up
    some internal logic and lowers the odds of runaway request contexts
    in unittests.
-   Fixed the Jinja2 environment쯵 좋list_templates좋 method not
    returning the correct names when blueprints or modules were
    involved.


Version 0.7.2
-------------

Released 2011-07-06

-   Fixed an issue with URL processors not properly working on
    blueprints.


Version 0.7.1
-------------

Released 2011-06-29

-   Added missing future import that broke 2.5 compatibility.
-   Fixed an infinite redirect issue with blueprints.


Version 0.7
-----------

Released 2011-06-28, codename Grappa

-   Added :meth:�~flask.Flask.make_default_options_response� which can
    be used by subclasses to alter the default behavior for 좋OPTIONS좋
    responses.
-   Unbound locals now raise a proper :exc:핾untimeError� instead of an
    :exc:핤ttributeError�.
-   Mimetype guessing and etag support based on file objects is now
    deprecated for :func:햒lask.send_file� because it was unreliable.
    Pass filenames instead or attach your own etags and provide a proper
    mimetype by hand.
-   Static file handling for modules now requires the name of the static
    folder to be supplied explicitly. The previous autodetection was not
    reliable and caused issues on Google쯵 App Engine. Until 1.0 the old
    behavior will continue to work but issue dependency warnings.
-   Fixed a problem for Flask to run on jython.
-   Added a 좋PROPAGATE_EXCEPTIONS좋 configuration variable that can be
    used to flip the setting of exception propagation which previously
    was linked to 좋DEBUG좋 alone and is now linked to either 좋DEBUG좋
    or 좋TESTING좋.
-   Flask no longer internally depends on rules being added through the
    좋add_url_rule좋 function and can now also accept regular werkzeug
    rules added to the url map.
-   Added an 좋endpoint좋 method to the flask application object which
    allows one to register a callback to an arbitrary endpoint with a
    decorator.
-   Use Last-Modified for static file sending instead of Date which was
    incorrectly introduced in 0.6.
-   Added 좋create_jinja_loader좋 to override the loader creation
    process.
-   Implemented a silent flag for 좋config.from_pyfile좋.
-   Added 좋teardown_request좋 decorator, for functions that should run
    at the end of a request regardless of whether an exception occurred.
    Also the behavior for 좋after_request좋 was changed. It쯵 now no
    longer executed when an exception is raised. See
    :ref:햡pgrading-to-new-teardown-handling�
-   Implemented :func:햒lask.has_request_context�
-   Deprecated 좋init_jinja_globals좋. Override the
    :meth:�~flask.Flask.create_jinja_environment� method instead to
    achieve the same functionality.
-   Added :func:햒lask.safe_join�
-   The automatic JSON request data unpacking now looks at the charset
    mimetype parameter.
-   Don쯶 modify the session on :func:햒lask.get_flashed_messages� if
    there are no messages in the session.
-   좋before_request좋 handlers are now able to abort requests with
    errors.
-   It is not possible to define user exception handlers. That way you
    can provide custom error messages from a central hub for certain
    errors that might occur during request processing (for instance
    database connection errors, timeouts from remote resources etc.).
-   Blueprints can provide blueprint specific error handlers.
-   Implemented generic :ref:햢iews� (class-based views).


Version 0.6.1
-------------

Released 2010-12-31

-   Fixed an issue where the default 좋OPTIONS좋 response was not
    exposing all valid methods in the 좋Allow좋 header.
-   Jinja2 template loading syntax now allows "./" in front of a
    template load path. Previously this caused issues with module
    setups.
-   Fixed an issue where the subdomain setting for modules was ignored
    for the static folder.
-   Fixed a security problem that allowed clients to download arbitrary
    files if the host server was a windows based operating system and
    the client uses backslashes to escape the directory the files where
    exposed from.


Version 0.6
-----------

Released 2010-07-27, codename Whisky

-   After request functions are now called in reverse order of
    registration.
-   OPTIONS is now automatically implemented by Flask unless the
    application explicitly adds 쯓PTIONS� as method to the URL rule. In
    this case no automatic OPTIONS handling kicks in.
-   Static rules are now even in place if there is no static folder for
    the module. This was implemented to aid GAE which will remove the
    static folder if it쯵 part of a mapping in the .yml file.
-   The :attr:�~flask.Flask.config� is now available in the templates as
    좋config좋.
-   Context processors will no longer override values passed directly to
    the render function.
-   Added the ability to limit the incoming request data with the new
    좋MAX_CONTENT_LENGTH좋 configuration value.
-   The endpoint for the :meth:햒lask.Module.add_url_rule� method is now
    optional to be consistent with the function of the same name on the
    application object.
-   Added a :func:햒lask.make_response� function that simplifies
    creating response object instances in views.
-   Added signalling support based on blinker. This feature is currently
    optional and supposed to be used by extensions and applications. If
    you want to use it, make sure to have 햍linker�_ installed.
-   Refactored the way URL adapters are created. This process is now
    fully customizable with the :meth:�~flask.Flask.create_url_adapter�
    method.
-   Modules can now register for a subdomain instead of just an URL
    prefix. This makes it possible to bind a whole module to a
    configurable subdomain.

.. _blinker: https://pypi.org/project/blinker/


Version 0.5.2
-------------

Released 2010-07-15

-   Fixed another issue with loading templates from directories when
    modules were used.


Version 0.5.1
-------------

Released 2010-07-06

-   Fixes an issue with template loading from directories when modules
    where used.


Version 0.5
-----------

Released 2010-07-06, codename Calvados

-   Fixed a bug with subdomains that was caused by the inability to
    specify the server name. The server name can now be set with the
    좋SERVER_NAME좋 config key. This key is now also used to set the
    session cookie cross-subdomain wide.
-   Autoescaping is no longer active for all templates. Instead it is
    only active for 좋.html좋, 좋.htm좋, 좋.xml좋 and 좋.xhtml좋. Inside
    templates this behavior can be changed with the 좋autoescape좋 tag.
-   Refactored Flask internally. It now consists of more than a single
    file.
-   :func:햒lask.send_file� now emits etags and has the ability to do
    conditional responses builtin.
-   (temporarily) dropped support for zipped applications. This was a
    rarely used feature and led to some confusing behavior.
-   Added support for per-package template and static-file directories.
-   Removed support for 좋create_jinja_loader좋 which is no longer used
    in 0.5 due to the improved module support.
-   Added a helper function to expose files from any directory.


Version 0.4
-----------

Released 2010-06-18, codename Rakia

-   Added the ability to register application wide error handlers from
    modules.
-   :meth:�~flask.Flask.after_request� handlers are now also invoked if
    the request dies with an exception and an error handling page kicks
    in.
-   Test client has not the ability to preserve the request context for
    a little longer. This can also be used to trigger custom requests
    that do not pop the request stack for testing.
-   Because the Python standard library caches loggers, the name of the
    logger is configurable now to better support unittests.
-   Added 좋TESTING좋 switch that can activate unittesting helpers.
-   The logger switches to 좋DEBUG좋 mode now if debug is enabled.


Version 0.3.1
-------------

Released 2010-05-28

-   Fixed a error reporting bug with :meth:햒lask.Config.from_envvar�
-   Removed some unused code from flask
-   Release does no longer include development leftover files (.git
    folder for themes, built documentation in zip and pdf file and some
    .pyc files)


Version 0.3
-----------

Released 2010-05-28, codename Schnaps

-   Added support for categories for flashed messages.
-   The application now configures a :class:햘ogging.Handler� and will
    log request handling exceptions to that logger when not in debug
    mode. This makes it possible to receive mails on server errors for
    example.
-   Added support for context binding that does not require the use of
    the with statement for playing in the console.
-   The request context is now available within the with statement
    making it possible to further push the request context or pop it.
-   Added support for configurations.


Version 0.2
-----------

Released 2010-05-12, codename J?germeister

-   Various bugfixes
-   Integrated JSON support
-   Added :func:�~flask.get_template_attribute� helper function.
-   :meth:�~flask.Flask.add_url_rule� can now also register a view
    function.
-   Refactored internal request dispatching.
-   Server listens on 127.0.0.1 by default now to fix issues with
    chrome.
-   Added external URL support.
-   Added support for :func:�~flask.send_file�
-   Module support and internal request handling refactoring to better
    support pluggable applications.
-   Sessions can be set to be permanent now on a per-session basis.
-   Better error reporting on missing secret keys.
-   Added support for Google Appengine.


Version 0.1
-----------

Released 2010-04-16

-   First public preview release.
