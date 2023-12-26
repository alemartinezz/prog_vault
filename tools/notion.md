# Notion formulas

## Calculate time formula

```js
if(empty(prop("Due")),
    "",
    (
        (
            if(prop("Status") == "Done",
                "✅ ",
                if(prop("Due") > now(),
                    "⏰ ",
                    "⌛️ "
                )
            )
        ) +
        if((dateBetween(now(), prop("Due"), "years") != 0),
            (
                format(abs(dateBetween(now(), prop("Due"), "years"))) +
                if((abs(dateBetween(now(), prop("Due"), "years")) == 1),
                    " year",
                    " years"
                )
            ),
            ""
        ) +
        if(((abs(dateBetween(now(), prop("Due"), "months")) % 12) != 0),
            (
                (if((dateBetween(now(), prop("Due"), "years") != 0),
                    ", ",
                    ""
                ) +
                format(abs(dateBetween(now(), prop("Due"), "months")) % 12)) +
                if(((abs(dateBetween(now(), prop("Due"), "months")) % 12) == 1),
                    " month",
                    " months"
                )
            ),
            ""
        ) +
        if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0),
            (
                (if(((dateBetween(now(), prop("Due"), "months") % 12) != 0),
                    ", ",
                    (if((dateBetween(now(), prop("Due"), "years") != 0),
                        ", ",
                        ""
                    ))
                ) +
                format((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30)) +
                if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) == 1),
                    " day",
                    " days"
                )
            ),
            ""
        ) +
        if(((abs(dateBetween(now(), prop("Due"), "hours")) % 24) != 0),
            (
                (if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0),
                    ", ",
                    (if(((dateBetween(now(), prop("Due"), "months") % 12) != 0),
                        ", ",
                        (if((dateBetween(now(), prop("Due"), "years") != 0),
                            ", ",
                            ""
                        ))
                    ))
                ) +
                format(abs(dateBetween(now(), prop("Due"), "hours")) % 24)) + " hr"
            ),
            ""
        ) +
        if((((abs(dateBetween(now(), prop("Due"), "minutes")) - (abs(dateBetween(now(), prop("Due"), "hours")) * 60)) % 60) != 0),
            (
                (if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0),
                    ", ",
                    (if(((dateBetween(now(), prop("Due"), "months") % 12) != 0),
                        ", ",
                        (if((dateBetween(now(), prop("Due"), "years") != 0),
                            ", ",
                            (if(((abs(dateBetween(now(), prop("Due"), "hours")) % 24) != 0),
                                ", ",
                                ""
                            ))
                        ))
                    ))
                ) +
                format((abs(dateBetween(now(), prop("Due"), "minutes")) - (abs(dateBetween(now(), prop("Due"), "hours")) * 60)) % 60)) + " min"
            ),
            ""
        ) +
        if((now() > prop("Due")),
            (
                if((abs(dateBetween(now(), prop("Due"), "minutes")) > 0),
                    " ago",
                    " justnow"
                )
            ),
            " left"
        )
    )
)
```

Condensed

```js
if(empty(prop("Due")), "", ((if(prop("Status") == "Done", "✅ ", if(prop("Due") > now(), "⏰ ", "⌛️ " ))) + if((dateBetween(now(), prop("Due"), "years") != 0), (format(abs(dateBetween(now(), prop("Due"), "years"))) + if((abs(dateBetween(now(), prop("Due"), "years")) == 1), " year", " years")), "" ) + if(((abs(dateBetween(now(), prop("Due"), "months")) % 12) != 0), ((if((dateBetween(now(), prop("Due"), "years") != 0), ", ", "") + format(abs(dateBetween(now(), prop("Due"), "months")) % 12)) + if(((abs(dateBetween(now(), prop("Due"), "months")) % 12) == 1), " month", " months")), "" ) + if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0), ((if(((dateBetween(now(), prop("Due"), "months") % 12) != 0), ", ", (if((dateBetween(now(), prop("Due"), "years") != 0), ", ", "" ))) + format((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30)) + if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) == 1), " day", " days" )), "" ) + if(((abs(dateBetween(now(), prop("Due"), "hours")) % 24) != 0), ((if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0), ", ", (if(((dateBetween(now(), prop("Due"), "months") % 12) != 0), ", ", (if((dateBetween(now(), prop("Due"), "years") != 0), ", ", "" ))))) + format(abs(dateBetween(now(), prop("Due"), "hours")) % 24)) + " hr" ), "" ) + if((((abs(dateBetween(now(), prop("Due"), "minutes")) - (abs(dateBetween(now(), prop("Due"), "hours")) * 60)) % 60) != 0), ( (if((((abs(dateBetween(now(), prop("Due"), "days")) % 365) % 30) != 0), ", ", (if(((dateBetween(now(), prop("Due"), "months") % 12) != 0), ", ", (if((dateBetween(now(), prop("Due"), "years") != 0), ", ", (if(((abs(dateBetween(now(), prop("Due"), "hours")) % 24) != 0), ", ", "" ))))))) + format((abs(dateBetween(now(), prop("Due"), "minutes")) - (abs(dateBetween(now(), prop("Due"), "hours")) * 60)) % 60)) + " min" ), "" ) + if((now() > prop("Due")), (if((abs(dateBetween(now(), prop("Due"), "minutes")) > 0), " ago", " just now")), " left")))
```
