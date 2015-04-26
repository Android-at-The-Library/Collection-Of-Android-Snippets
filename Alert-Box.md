## Alert-Box

Sometimes will want a pop-up, below is the snippet code.

Probably would be good to put it into it's own helper method.

```java
 AlertDialog.Builder alert_builder = new AlertDialog.Builder(this);
 
        alert_builder
                .setTitle("This is an Alert Box") //change this
                .setMessage("I wanted you to know something, and so I made this alert :D")
                .setPositiveButton("Confirm", new DialogInterface.OnClickListener() {
                    public void onClick(DialogInterface dialog, int id) {
                        dialog.cancel();
                    }
                });
 
        AlertDialog dialog = alert_builder.create();
        dialog.show();
```
