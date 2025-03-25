
This talk will be a quick (20 minute) introduction to the Jakarta EE TCK projects like https://github.com/jakartaee/platform-tck/

- 1. Purpose of EE TCKs (test compatibility kits)
	- Validate that Jakarta EE implementations correctly implement the Jakarta EE Specifications (e.g. Plaform, Web Profile, Persistence, CDI, Servlet, ...)
	- Is 100% of the Specification requirements tested and is 100% of APIs tested?
		- No, only the most difficult to implement aspects are tested.
	- How long does it take to run the EE TCKs?
		- Not sure but we once calculated it would take around 3 days on a single computer with earlier EE versions.  With WildFly + Jakarta EE 10, it takes around 6-9 hours to run on multiple (CI) virtual machines.

---

![Jakarta EE Compatible implementations](https://jakarta.ee/images/jakarta/jakarta-ee-compatible-logo-color.svg "Jakarta EE Compatible implementations")
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;

- 2. Relationship between the TCK tests and your applications
	- How do applications benefit from WildFly passing TCK tests?
		- Ensures that applications written to the EE specs are (somewhat) portable to different Jakarta EE implementations.
		- Why exactly only somewhat portable?
			- The TCK tests the difficult to implement parts of EE but not all of EE is tested.
		- Can you add tests to the EE TCKs?
			- Yes you can add new tests for the next EE release being developed.  This will soon be Jakarta EE 12.  See the next slide for more information.

---

![Platform TCK repository](https://github.com/scottmarlow/talks/raw/refs/heads/main/platformtckrepo.png "Platform TCK repository")

- 3. How to ensure your application is portable to different EE implementations
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

![Platform TCK repository](https://github.com/scottmarlow/talks/raw/refs/heads/main/platformtckrepo.png "Platform TCK repository")
- 4. Deeper dive into TCKs
	- Prove that Persistence (EE) container can access third party persistence provider https://github.com/jakartaee/platform-tck/blob/main/tcks/apis/persistence/persistence-inside-container/platform-tests/src/main/java/ee/jakarta/tck/persistence/ee/pluggability/contracts/resource_local/Client.java#L77
		- @testName: createEMF @assertion_ids: PERSISTENCE:JAVADOC:1479; PERSISTENCE:SPEC:981; PERSISTENCE:SPEC:982
			- What is an assertion_id???
			- See map from ^ ID to JavaDoc via https://github.com/jakartaee/platform-tck/blob/main/tcks/apis/persistence/persistence-inside-container/docs/assertions/2.0/PersistenceJavaDocAssertions_2_0.xml
			- See map from ^ ID to Spec via https://github.com/jakartaee/platform-tck/blob/main/tcks/apis/persistence/persistence-inside-container/docs/assertions/2.0/PersistenceSpecAssertions_2_0.xml
				- PERSISTENCE:SPEC:981 = "The interface jakarta.persistence.spi.PersistenceProvider is implemented by the persistence provider"
				- PERSISTENCE:JAVADOC:1479 = "Called by the container when an EntityManagerFactory is to be created."
				- some other details are also added as well.
		- The test assertion ids give an idea of which Jakarta EE Specification or JavaDoc (really SPEC API) requirement is tested by a TCK test.
		- As you can see from the above links it is not that easy to locate the reason why a test was added to the TCK.
		- https://github.com/jakartaee/platform-tck/issues/2006 is for adding an TCK AssertionID annotation that can instead be used in newly added tests
			- Perhaps ^ can be based on "Test Assertions Guidelines" http://docs.oasis-open.org/tag/guidelines/v1.0/cn02/guidelines-v1.0-cn02.pdf 

---

![Resource links](https://github.com/scottmarlow/talks/raw/refs/heads/main/links.png "Resource links")

-  4. Resources
	- Sign up for the Platform TCK mailing list https://accounts.eclipse.org/mailing-list/jakartaee-tck-dev 
	- Sign up for other Jakarta EE mailing lists https://jakarta.ee/connect/mailing-lists/
	- Platform TCK mailing list https://github.com/jakartaee/platform-tck
	- Platform TCK project page https://projects.eclipse.org/projects/ee4j.jakartaee-tck
	- Jakarta EE Specifications https://jakarta.ee/specifications/

