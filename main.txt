import requests as r
import threading
import keepalive
while True:
  threadAmount = 100
  threadLimit = 300
  i = 1

  def ping():
    global i
    for i in range(threadLimit):
      r.get(
        "https://camo.githubusercontent.com/17834254c4791ec01e19c536bf951860ae902e671ee28eb1f2e46540575bbc2f/68747470733a2f2f677076632e6172747572696f2e6465762f486f74646f67393939"
      )
      keepalive.keep_alive()
      print(f"gotcha {i}")
      i += 1

  threads = []
  for i in range(threadAmount):
    threads.append(threading.Thread(target=ping))

  for i in range(threadAmount):
    threads[i].start()

  for i in range(threadAmount):
    threads[i].join()
  print("Finish")
