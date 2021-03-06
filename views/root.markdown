## Available Methods :: Miscelleneous

- __IP Address and Environment__: returns the remote ip address as well
  as other environment variables for the current request.

        GET /ip                # json data
        GET /ip?format=plain   # plain text data

## Available Methods :: Github

All of the following methods expect a `user` (Github user to query data
for) and `token` (Github token for API authentication) parameter in the
`GET` request.

### Charts

- __Issues Burnout__: returns issues pending per day (cumulative) for
  the given user (uses filter: `all` from the API).

        GET /github/charts/issues_burnout

### Statistics

- __Contributions__: returns daily, weekly and monthly contributions
  (public) made on Github by the user, as well as, last contribution
  date, total contributions made and contribution streak for given user.
  Data is scraped by requesting:
  `http://github.com/users/<user>/contributions`

        GET /github/stats/contributions

- __Gists__: returns gists updated in the last week, month and the year
  by the user, as well as since the beginning grouped by `updated_at`.
  A different grouping method can be requested by adding `&group_by=`
  parameter.

        GET /github/stats/gists

- __Repos__: returns repositories grouped by `pushed_at` field in
  a daily, monthly, weekly and yearly graph data form. A different
  grouping method can be requested by adding `&group_by` parameter.

        GET /github/stats/repos

- __Open Issues__: returns open issues grouped by `updated_at` field in 
  a daily, monthly, weekly and yearly graph data form. A different
  grouping method can be requested by adding `&group_by` parameter.

        GET /github/stats/open_issues

- __Issues__: returns open and closed issues grouped by `updated_at`
  field in a daily, monthly, weekly and yearly graph data form.
  A different grouping method can be requested by adding `&group_by`
  parameter. Note that this method is really expensive, and should only
  be called when required.

        GET /github/stats/issues

### Listing

- __Repos__: returns list of repos for the given user.

        GET /github/lists/repos

- __Gists__: returns list of gists for the given user.

        GET /github/lists/gists

- __Open Issues__: returns list of open issues for the given user across
  all repositories.

        GET /github/lists/open_issues

### Combined method

You can request all the data that you need in a single request to this server by using the following method. Provide a comma separated list of methods that you need to access to this method.

        GET /github/charts/issues_burnout/stats/gists,contributions/lists/repos?user=<user>&token=<token>

The above request will provide statistics for the gists, open issues, repos and contributions done by the user as well as a list of open issues for the given user in the following format:

        {
            "charts": {
                "issues_burnout": {
                    ...
                }
            },
            "stats": {
                "gists": {
                    ...
                },
                "contributions": {
                    ...
                }
            },
            "lists": {
                "repos": {
                    ...
                }
            }
        }
