Problem Statement
=================

Dependency resolution has been an issue for Python packaging ecosystem
as long as it ever existed.  Like other language-specific software repositories
(and unlike traditional Unix-like repositories), :term:`package indices
<Package Index>` for Python serves all :term:`releases <Release>` of each
:term:`project <Project>`.  Therefore, the dependency backtracking process
is left for package managers like pip_ to handle, which reportedly costs
`performance penalties`_ on end-users' machines.  While part of them could
be tackled via better optimization, it is inevitable that the backtracking
process will always be computationally and resourcefully expensive
due to `its complexity being NP-Hard`_.

In order to improve the general situations for end-users
(as well as CI/CD services), we can provide package indices that provide
:term:`distribution packages <Distribution Package>` being resolved
out of the box.  Since dependency resolution as a non-trivial task,
it is suggested that such index should be carefully managed by human,
in the same manner as often seen in Unix-like repositories.

This new kind of Python package index should be compatible with
the existing toolchain (e.g. pip_) which expects the standardized
`simple project API`_.  As this API is served through HTTP(S),
it is possible to store distributions on a distributed file system
like the :term:`InterPlanetary File System (IPFS)`, and preferably so
for the ease of mirroring.

Distribution packages will be submitted by contributors incrementally.
For each update (addition/upgrade/removal), proposals will be reviewed
by maintainers and automatically checked.  The purpose of these checks
is to make sure that new updates does not cause conflicts within
the package index, so that end-users can always pull working subsets
of distributions without having to performing dependency resolution
on their machine.

To maintain the authoritative permissions of contributors and maintainers,
a login system will need to be employed.  Contributors will be able
to submit new proposals and maintainers will have the authority to approve
or dismiss them.  Maintainers will have the ability to upload proposals as well.

New maintainers can be elected from the list of existing contributors.
Contributors will be able to nominate (or self-nominate) candidates
for new maintainers, but only maintainers can vote whether or not
the candidates will be promoted.

.. _pip: https://pip.pypa.io
.. _performance penalties: https://github.com/pypa/pip/issues/8664
.. _its complexity being NP-Hard: https://medium.com/@nex3/pubgrub-2fb6470504f
.. _simple project API:
   https://warehouse.readthedocs.io/api-reference/legacy/#simple-project-api
