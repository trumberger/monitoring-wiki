In order to better understand the underlying information we'll be working with, and how we are going to pre-process, we list possible metrics, KPIs and applicable analysis we could do on this information.

	• Define core scenarios
		□ Network
			§ Requests
			§ Load
			§ Backend traffic
			§ HTTP/S traffic
		○ Cloud
			§ Availability (outages)
			§ Latency
			§ Routing decisions
			§ Internal/External requests latency
			§ Cloud-to-Cloud and Onprem-to-Cloud timings (hybrid usage)
			§ IaaS
				□ VNET
				□ CPU (over/under utilization)
					® Server groups comparisons
					® Network routing issues
					® Application features usage
				□ Memory
				□ I/O
				□ Virtualization
			§ PaaS
				□ Network
					® Requests
					® Load
				□ Compute
				□ Process load
				□ Storage
				□ Bandwidth
					® Capacity
					® Consumption
				□ Quotas
		○ Server-based
			§ Network
				® Requests
				® Load
				® Backend traffic
				® HTTP/S traffic
			§ Database
				® Open connections
				® Queries
				® Response time
				® Data transfers
			§ Internet server
			§ Mail server
			§ Others
		○ Applications
			§ Exceptions
			§ Unusual server logs/web logs
			§ DB size growth rate
			§ DevOps activity
				® Deployments
				® Continuous delivery
				® Testing activity
			§ Application specific metrics
				® Specific transactions
	• RCA
		○ Define KPIs/evidence
			§ Thresholds
				□ Theoretical and practical limits
			§ Correlation
			§ Average
			§ Outliers
			§ Standard deviation
		○ Scenarios
			§ Uptime
			§ Outages
			§ Data loss
			§ Performance Degradation
		○ Causes
			§ Bayesian network
	• Classification Algorithms
	        § Clustering

Considering the information we would we able to gather from several sources, we might take each one of them and search for anomalies or inconsistencies between different sources, using Application Insights Analytics, and then with a Bayesian Network provide some early Root Cause Analysis (ref: [Root-Cause Analysis with In-Query Machine Learning in Application Insights Analytics](https://azure.microsoft.com/en-us/blog/root-cause-analysis-with-in-query-machine-learning-in-application-insights-analytics/))
