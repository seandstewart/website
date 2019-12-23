# Projects

## Software
A list of my open-source projects, all hosted on
[:fa-github: Github](https://github.com/seandstewart).

### typical
A Simple, Fast, & Correct suite of tools for run-time type-safety,
validation, schema definitions, and so much more, using
[PEP 484](https://www.python.org/dev/peps/pep-0484/) type hints.

- [Repository](https://github.com/seandstewart/typical)
- [Documentation](https://python-typical.org/)

```pydevconsole
>>> import typic
>>>
>>> @typic.al
>>> def hard_math(a: int, b: int) -> int:
...     return a % b
... 
>>> hard_math("1", 2.0)
1
```

### Qué
A tiny little library for composing SQL-compliant statements
dynamically and generating SQL statements from dataclasses.

- [Repository](https://github.com/seandstewart/que)

```pydevconsole
>>> import que
>>> import dataclasses
>>> import datetime
>>>
>>> @dataclasses.dataclass
... class Foo:
...     bar: str
...     id: int = None
...     created: datetime.datetime = None
... 
>>> new_foo = Foo('blah')
>>> fields = que.data_to_fields(new_foo, exclude=None)
>>> insert = que.Insert(table='foo', fields=fields)
>>> sql, args = insert.to_sql(que.NameParamStyle.NAME)
>>> print(sql)
INSERT INTO
  foo (:colbar)
VALUES
  (:valbar)

>>> args
{'colbar': 'bar', 'valbar': 'blah'}
```

### Iambic
A parsing and rendering library for spoken text and plays. Count
spoken lines, track characters, and more... 

- [Repository](https://github.com/seandstewart/iambic)

```pydevconsole
>>> import iambic
>>> play = """
... # ACT I
... ## SCENE I. A field.
... 
... _Enter FOO._
... 
... **FOO**
... Bar.
... 
... _Exeunt_
... """
...
>>> parsed = iambic.parse.text(play, title="Foo")
>>> print(parsed.json)
{
  "type":"play",
  "children":[
    {
      "type":"tree",
      "node":{
        "type":"act",
        "index":0,
        "text":"ACT I",
        "num":1
      },
      "children":[
        {
          "type":"tree",
          "node":{
            "type":"scene",
            "index":1,
            "text":"SCENE I",
            "num":1,
            "act":"act-i",
            "setting":null
          },
          "children":[
            {
              "type":"entrance",
              "index":2,
              "text":"Enter FOO.",
              "scene":"act-i-scene-i",
              "personae":[
                "foo"
              ]
            },
            {
              "type":"speech",
              "persona":"foo",
              "scene":"act-i-scene-i",
              "speech":[
                {
                  "type":"dialogue",
                  "line":"Bar.",
                  "persona":"foo",
                  "scene":"act-i-scene-i",
                  "index":4,
                  "lineno":1,
                  "linepart":0
                }
              ],
              "index":4
            },
            {
              "type":"exit",
              "index":5,
              "text":"Exeunt",
              "scene":"act-i-scene-i",
              "personae":[
              ]
            }
          ],
          "personae":[
            "foo"
          ]
        }
      ],
      "personae":[
      ]
    }
  ],
  "personae":[
    {
      "type":"persona",
      "index":3,
      "text":"FOO",
      "name":"Foo",
      "short":null
    }
  ],
  "meta":{
    "type":"meta",
    "rights":"Creative Commons Non-Commercial Share Alike 3.0",
    "language":"en-GB-emodeng",
    "publisher":"Published w\/ \u2764\ufe0f using iambic - https:\/\/pypi.org\/project\/iambic",
    "title":"Foo",
    "subtitle":null,
    "edition":1,
    "author":"William Shakespeare",
    "editors":[
    ],
    "tags":[
    ]
  }
}
```
