# Base
一些应用基类的抽取
import android.app.Application;

import android.content.Context;

import android.os.Handler;

public class MyApplication extends Application {

	//全局上下文环境
	private static Context mContext;
	
	//全局的handler
	private static Handler mHandler;
	
	//主线程
	private static Thread mMainThread;
	
	//主线程id
	private static int mMainThreadId;
	
	//此方法在其余代码运行前,就会调用,所有在此处去构建开发过程中需要用到的常见对象,并且提供方法用于获取
	@Override
	public void onCreate() {
		mContext = getApplicationContext();
		
		mHandler = new Handler();
		
		//MyApplication运行在主线程中,所以拿当前线程对象即可
		mMainThread = Thread.currentThread();
		
		//主线程id,就是MyApplication(主线程)线程id,获取当前线程id
		mMainThreadId = android.os.Process.myTid();
		
		super.onCreate();
	}

	public static Context getContext() {
		return mContext;
	}

	public static Handler getHandler() {
		return mHandler;
	}

	public static Thread getMainThread() {
		return mMainThread;
	}

	public static int getMainThreadId() {
		return mMainThreadId;
	}
	
}

