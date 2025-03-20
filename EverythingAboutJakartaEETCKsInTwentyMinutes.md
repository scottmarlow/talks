
This talk will be a quick (20 minute) introduction to the Jakarta EE TCK projects like https://github.com/jakartaee/platform-tck/

- Purpose of EE TCKs (test compatibility kits)
	- Validate that Jakarta EE implementations correctly implement the Jakarta EE Specifications (e.g. Plaform, Web Profile, Persistence, CDI, Servlet, ...)
	- Is 100% of the Specification requirements tested and is 100% of APIs tested?
		- No, only the most difficult to implement aspects are tested.
	- How long does it take to run the EE TCKs?
		- Not sure but we once calculated it would take around 3 days on a single computer with earlier EE versions.  With WildFly + Jakarta EE 10, it takes around 6-9 hours to run on multiple (CI) virtual machines.

---










- Relationship between the TCK tests and your applications
	- How do applications benefit from WildFly passing TCK tests?
		- Ensures that applications written to the EE specs are (somewhat) portable to different Jakarta EE implementations.
		- Why exactly only somewhat portable?
			- The TCK tests the difficult to implement parts of EE but not all of EE is tested.
		- Can you add tests to the EE TCKs?
			- Yes you can add new tests for the next EE release being developed.  This will soon be Jakarta EE 12.  See the next slide for more information.

---










- How to ensure your application is portable to different EE implementations
	- More clearly, assume that your application depends on a Persistence SPEC API method foobar() and foobar doesn't work as described in the Persistence SPEC document.  Of course there is no foobar method but this is just an example.
		- You can create a https://github.com/jakartaee/platform-tck pull request to add a test for the foobar method that all Jakarta EE implementations will have to pass.  
			- Also sign the Eclipse contributor agreement (https://accounts.eclipse.org/user/eca) using your email address that you associated with your github account.
		- You can also open a WildFly issue on https://issues.jboss.org/browse/WFLY that Persistence foobar support needs to be fixed and why.
	- How can we make it easier to add new TCK tests
		- Some history:
			- For the past several years, the Java Test Harness and Apache Ant has worked very well for running TCK tests but very few people understand how to add TCK tests.
				- OpenJDK still uses the [JTHarness](https://github.com/openjdk/jtharness) 
			- It is time to switch to more modern tools Like Maven + JUnit.
				- Jakarta EE 11 will use Maven + Junit for running TCKs.
			- Later for Jakarta EE 12 we will see how far we get with further improvements.

---










-  Resources
	- Sign up for the Platform TCK mailing list https://accounts.eclipse.org/mailing-list/jakartaee-tck-dev 
	- Sign up for other Jakarta EE mailing lists https://jakarta.ee/connect/mailing-lists/
	- Platform TCK mailing list https://github.com/jakartaee/platform-tck
	- Platform TCK project page https://projects.eclipse.org/projects/ee4j.jakartaee-tck
	- Jakarta EE Specifications https://jakarta.ee/specifications/
