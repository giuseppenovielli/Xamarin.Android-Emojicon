# Xamarin.Android-Emojicon
Xamarin.Android Binding of Emojicon library https://github.com/ankushsachdeva/emojicon by Giuseppe Novielli

# Usage EmojiconEditText

# XML Layout Fragment EmojiconEditText

       <github.ankushsachdeva.emojicon.EmojiconEditText
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:textSize="16dp"
                        android:id="@+id/emojiEditText"
                        android:hint="Write Text"
                        emojicon:emojiconSize="27dp"
                        android:minHeight="50dp"/>

# In a Fragment but is similar into Activity

       ...
     private EmojiconPopup _emojiconPopup;
    private EmojiconEditText _emojiconEditText;
    private Button _emojiBtn;
 
     public override View OnCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)
          {
          
        ....
           View fragmentView = inflater.Inflate(Resource.Layout.FragmentEmojicon, container, false);
           SetupEmojiconPopup(fragmentView);
           _emojiBtn.Click += _mEmojiBtn_Click;
           
        ......
        
        return fragmentView;
       }
 
  
    private void SetupEmojiconPopup(View viewFragment)
    {
     _emojiconPopup = new EmojiconsPopup(viewFragment, Activity);

            _emojiconPopup.SetSizeForSoftKeyboard();

            _emojiconPopup.EmojiconClicked += (sender, args) =>
            {
                _emojiconEditText.Append(args.P0.Emoji);
            };

            _emojiconPopup.EmojiconBackspaceClicked += (sender, args) =>
            {
                var keyEvent = new KeyEvent(0, 0, 0, Keycode.Del, 0, 0, 0, (int)Keycode.Endcall);
                _emojiconEditText.DispatchKeyEvent(keyEvent);
            };

            _emojiconPopup.DismissEvent += (sender, args) =>
            {
                <For Change icon _emojiBtn Keyboard-Emojicon>
            };

            _emojiconPopup.KeyboardClose += (sender, args) =>
            {
                if (_emojiconPopup.IsShowing)
                {
                    _emojiconPopup.Dismiss();
                }
            };
        }
  
  
  
    private void _mEmojiBtn_Click(object sender, EventArgs e)
        {
        
        //Show, Close Emoji Keyboard
            if (!_emojiconPopup.IsShowing)
            {

                if (_emojiconPopup.IsKeyBoardOpen().BooleanValue())
                {

                    _emojiconPopup.ShowAtBottom();
                    <Change icon _emojiBtn = Keyboard>

                }
                else
                {

                    _emojiconEditText.FocusableInTouchMode = true;
                    _emojiconEditText.RequestFocus();
                    _emojiconPopup.ShowAtBottomPending();

                    var inputMethodManager = Activity.GetSystemService(Context.InputMethodService) as InputMethodManager;
                    inputMethodManager.ShowSoftInput(_mCommentEdit, Android.Views.InputMethods.ShowFlags.Implicit);
                    <Change icon _emojiBtn = Emoji>
                }

            }
            else
            {

                _emojiconPopup.Dismiss();
            }
        }
        
  # Available NuGet
  https://www.nuget.org/packages/Xamarin.Android.Emojicon/
