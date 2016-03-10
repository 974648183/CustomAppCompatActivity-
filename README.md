# CustomAppCompatActivity-
解决2个或多个Fragment嵌套时onActivityResult不被调用的解决方案 

然后我们的Activity继承这个CustomAppCompatActivity即可，但是要注意，在Fragment中调用startActivityForResult时，一定要调用根Fragment的启动方法，如下：

/**
  * 得到根Fragment
  * 
  * @return
  */
 private Fragment getRootFragment() {
  Fragment fragment = getParentFragment();
  while (fragment.getParentFragment() != null) {
   fragment = fragment.getParentFragment();
  }
  return fragment;

 }

 /**
  * 启动Activity
  */
 private void onClickTextViewRemindAdvancetime() {
  Intent intent = new Intent();
  intent.setClass(getActivity(), YourActivity.class);
  intent.putExtra("TAG","TEST"); 
  getRootFragment().startActivityForResult(intent, 1000);
 }
