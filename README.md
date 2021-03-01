# Brief.me Guidelines
Guidelines used in Brief.me private and public projects. This document aims at :
* Improving consistency intra- and inter-projects.
* Taking tangible decisions.
* Having a reference document to refer to.
* Helping new developers working on our projects.

Those guidelines are constantly evolving and are the results of discussions 
from Brief.me's tech team and outside collaborators.

## Coding style (Django)
### Views
#### Decorators
Decorators should be placed at the method level when it exists and 
at the class level otherwise.
```python
class DummyView(View):
    
    @method_decorator(login_required)
    def dispatch(self, request, *args, **kwargs):
        if request.user.is_active:
            return HttpResponseForbidden("already active")
        return super().dispatch(request, *args, **kwargs)

...

@method_decorator(login_required, name="dispatch")
class ChangePasswordView(FormView):

    form_class = ChangePasswordForm
    template_name = "account/change_password.html"
```

When having the choice between a mixin and a decorator 
for the same functional need, we should use the decorator
(e.g.: `LoginRequiredMixin` mixin and `login_required` decorator)

### Chargify calls
When calling an endpoint to the Chargify's API, we should always use the methods within the `ChargifyHelper` class.
`chargify_python` should only be used within `ChargifyHelper` methods.


## Commit formatting
The philosophy of this specification is based on [conventional commits](https://www.conventionalcommits.org/en/).
We adapted it to fit our business needs and habits.

Here is the list of verbs with their usage that must be used in our projects:

| Verbs         | Usage                                                                             |
| ------------- |:---------------------------------------------------------------------------------:|
| fix           | Patch a bug                                                                       |
| feat          | Add new feature                                                                   |
| refactor      | A code change that neither fixes a bug nor adds a feature                         |
| style         | Changes that do not affect the meaning of the code (white-space, formatting, ...) |
| docs          | Documentation only changes                                                        |
| chore         | Changes to configuration files (CI, Makefile, pytest.ini, black.toml, ...)        |
| test          | Adding missing tests or correcting existing tests                                 |
