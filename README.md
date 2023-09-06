this package does nothing, but used to demonstrate the importance of correctly specifying git repo dependencies in poetry.

to point: if two (poetry) packages -- say `package-a` and `package-b` -- both depend on this one, but one of them specifies the dependency as
```
poetry add git+https://github.com/abefrandsen/shared_dependency.git
```
and the other specifies the dependency as
```
poetry add git+https://github.com/abefrandsen/shared_dependency
```
you will encounter problems when trying to create a poetry environment that depends both on `package-a` and `package-b`.
You will encounter something like the following error:
```
Because depend-b (0.1.0) @ git+https://github.com/abefrandsen/depend_B.git@HEAD depends on shared-dependency (0.1.0) @ git+https://github.com/abefrandsen/shared_dependency.git
 and depend-a (0.1.0) @ git+https://github.com/abefrandsen/depend_A.git@HEAD depends on shared-dependency (0.1.0) @ git+https://github.com/abefrandsen/shared_dependency, depend-b (0.1.0) @ git+https://github.com/abefrandsen/depend_B.git@HEAD is incompatible with depend-a (0.1.0) @ git+https://github.com/abefrandsen/depend_A.git@HEAD.
So, because testing depends on both depend-a (0.1.0) @ git+https://github.com/abefrandsen/depend_A.git and depend-b (0.1.0) @ git+https://github.com/abefrandsen/depend_B.git, version solving failed.
```
