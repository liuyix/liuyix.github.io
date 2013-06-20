---
comments: true
published: false
date: 2012-06-06 10:46:50
layout: post
slug: android-customize-exit-operation
title: Android界面退出的监听——实现“确认退出”对话框
wordpress_id: 664
categories:
- android
tags:
- android
- basic
---

方法有两种：



	
  1. Android所有版本通用：重写`public boolean onKeyDown(int keyCode, KeyEvent event)`

	
  2. Android API Level 5以上可用：重写`public void onBackPressed() `



以下为示例：
方法一：
在你的Activity中插入以下代码：

    
    
        @Override
        public void onBackPressed() {
    	new AlertDialog.Builder(this).setTitle("确认退出吗？")
    		.setIcon(android.R.drawable.ic_dialog_info)
    		.setPositiveButton("确定", new DialogInterface.OnClickListener() {
    
    		    @Override
    		    public void onClick(DialogInterface dialog, int which) {
    			// 点击“确认”后的操作
    			MainFragmentActivity.this.finish();
    
    		    }
    		})
    		.setNegativeButton("返回", new DialogInterface.OnClickListener() {
    
    		    @Override
    		    public void onClick(DialogInterface dialog, int which) {
    			// 点击“返回”后的操作,这里不设置没有任何操作
    		    }
    		}).show();
    	// super.onBackPressed();
        }
    



方法二：

    
    
        @Override
        public boolean onKeyDown(int keyCode, KeyEvent event) {
    	if (keyCode == KeyEvent.KEYCODE_BACK) {//KeyEvent.KEYCODE_BACK即是back键对应的code
    	    Toast.makeText(this, "Back key pressed!", Toast.LENGTH_SHORT).show();//当back键按下的时候会弹出Toast提示，你也可以将上一示例的对话框加入下来
    	    return true;//返回true表示该事件已被处理，不会再传递到次级监听者;返回false表示该事件还没有被处理完，会继续传递给其他监听者
    	}
    	return false;//如果按下的是其他按键则直接返回false表示该事件没有处理。
        }
    
