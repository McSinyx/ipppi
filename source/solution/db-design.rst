Database Design
===============

..uml..

  !define primary_key(x) <u>x</u>

  entity "package" as pkg{
    primary_key(pkg:text)
    version:text
    url:text
  }
  entity "dependency" as dp{
    primary_key(pkg:text)
    requirement:text
  }
  entity "proposal" as pp{
    primary_key(uuid:text)
    proposer:text
    conflict:BOOL
  }
  entity "whlupdate" as whl{
    primary_key(uuid:text)
    primary_key(pkg:text)
    whl:text
  }
  entity "account" as acc{
    primary_key(username:text)
    password:text
    maintainer:BOOL
  }
  pkg ||--|| dp
  pkg }|--||whl
  whl||--|{pp
