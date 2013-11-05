Heroku
======

Resource not found
------------------

The second time I create a heroku app, I skipped the step-by-step tutorial. After adding the remote to git, pushing code to the repository, there was simply no web dyno showing up in the dashboard but the error message in ``heroku logs``: ``at=error code=H14 desc="No web processes running``, and ``heroku ps:scale web=1`` returns ``!    Resource not found``.

Finally I realized the problem is a missing ``Procfile``. Add ``web: node app`` to ``Procfile`` solves the problem.