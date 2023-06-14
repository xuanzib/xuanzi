# xuanzi
package com.sun.content.server.operator.security.adaptor; 
 
import java.util.*; 
 
//import Content Delivery Server libraries 
import com.sun.content.server.service.security.*; 
import com.sun.content.server.service.security.util.*; 
 
//import here operator required packages 
// ....... 
 
public class SampleUserManagerImpl { 
 
	private SampleExternalProxy proxy; 
 
	public SampleUserManagerImpl() throws UserProfileResourceException { 
		 
		try { 
			init();			 
		} catch (Exception ex) { 
				throw new com.sun.content.server.service.security.util.UserProfileResourceException( "Failed to instantiate SampleUserManagerImpl ", ex); 
		} 
	} 
 
	// This method will create an External Directory Server Proxy and 
  // initiatlize this User Manager 
		private void init() throws UserProfileResourceException 
	{	 
		System.out.println("Initializing External UserManager .... "); 
		 
		try { 
			proxy = new SampleExternalProxy(); 
		} catch (Exception ex) { 
			System.out.println("Fatal Error " + ex.toString()); 
			throw new com.sun.content.server.service.security.util.UserProfileResourceException(ex.toString()); 
		} 
	} 
 
	protected boolean doIsAuthenticated(String inUserId, String inPassword) 
			throws UserProfileResourceException { 
				 	 
		System.out.println("SampleUserManagerImpl.doIsAuthenticated --- ");  
 
		boolean isauthenticated = false; 
		 
		try { 
    
			User aUser = proxy.createUserFromExternal(inUserId); 
			isauthenticated = ( (aUser.getLoginId()==inUserId) && (aUser.getPassword()==inPassword)); 
			if (isauthenticated) 
				System.out.println("SampleUserManagerImpl.doIsAuthenticated:- User "+inUserId+" is successfully authenticated."); 
			else 
				System.out.println("SampleUserManagerImpl.doIsAuthenticated:- User "+inUserId+" :unable to authenticate (wrong login and password)"); 
		} catch (Exception ex) { 
			isauthenticated = false; 
			System.out.println("SampleUserManagerImpl.doIsAuthenticated:- User "+inUserId+" can not authenticate (user not found)"); 
			throw new com.sun.content.server.service.security.util.UserProfileResourceException(ex.toString()); 
		} 
		return isauthenticated; 
								 
	} 
 
	protected boolean doAccountExists(String userId) throws UserProfileResourceException { 
	 
		System.out.println("SampleUserManagerImpl.doAccountExists --- ");  
		    
		// Use the External Proxy search method to check if the account exist 
		return proxy.searchUser(userId); 
	} 
  	 
  	 
  	protected boolean doAddUser(User user) throws UserProfileResourceException{ 
		 
		boolean updated = false; 
		 
		//This is not an allowed operation.If this is not the case add the code to 
    // implement it 
		System.out.println("SampleUserManagerImpl.doAddUser - This operation is not implemented !");  
		 
		return updated; 
 
  	}   
 
	protected void doDisableUser(String userId) throws UserProfileResourceException { 
	 
		//This is not an allowed operation.If this is not the case add the code to 
    // implement it 
		System.out.println("SampleUserManagerImpl.doDisableUser - This operation is not implemented !");  
		 
	} 
 
