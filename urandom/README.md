We note (from `ltrace`) that the program reads 10 bytes from `/dev/urandom`, and
checks if the first argument matches. However, it compares `strlen([bytes])`
bytes, so we can supply a short argument and run the program until the bytes
from `/dev/urandom` start with that argument + a null.

Final command: `while true; do ./urandom a; done;`
