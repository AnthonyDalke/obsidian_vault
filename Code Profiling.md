- pyinstrument presented as recommended tool
	- Aims to systematically focus on bottlenecks
	- Rather than sequentially measuring individual function calls, it samples full execution ever 1 ms
	- Run with `pyinstrument script.py`
	- Output in HTML, JSON, custom renderers, and other options
	- Even profile pytest test suites with `python -m pytest`
- To profile specific functions or methods, use context
	```python
	import pyinstrument
	
	def load_orders():
		...
		
	with pyinstrument.profile():
		orders = load_orders()
		total = sum(order["amount"] for order in orders)
	
	print(total)
	```
- Another use case involves calling the profiler directly within code
```python
def compute_slow_report():
	...
	
profiler = Profiler() # imported from pyinstrument
profiler.start()

result = compute_slow_report()

profiler.stop()
```