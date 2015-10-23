### 11.10\. Trying a Possible Solution

So, as we <a name="iddle2648"></a><a name="iddle2649"></a><a name="iddle2650"></a><a name="iddle2651"></a><a name="iddle2652"></a>have seen, <tt>bonobo_window_add_popup</tt> is an expensive function that must be called every time we want to create a pop-up menu. If we are repeatedly calling it with the same parameters, it may be possible to cache the value it returns from the initial call and use that every time after that instead of repeatedly calling that expensive function. [Listing 11.19](ch11lev1sec10.html#ch11ex19) shows an example of a rewritten function to do just that.

<a name="ch11ex19"></a>

##### Listing 11.19\.

<pre>void

fm_directory_view_pop_up_background_context_menu (FMDirectoryView *view,

                                        GdkEventButton *event)

{

   /* Primitive Cache */

   static FMDirectoryView *old_view = NULL;

   static GtkMenu *old_menu = NULL;

   g_assert (FM_IS_DIRECTORY_VIEW (view));

   /* Make the context menu items not flash as they update to proper disabled,

    * etc. states by forcing menus to update now.

    */

   if ((old_view != view)  ||  view->details->menu_states_untrustworthy)

          {

              update_menus_if_pending (view);

              old_view = view;

              old_menu = create_popup_menu(view, FM_DIRECTORY_VIEW_POPUP_PATH_BACKGROUND);

          }

  eel_pop_up_context_menu (old_menu,

         EEL_DEFAULT_POPUP_MENU_DISPLACEMENT,

         EEL_DEFAULT_POPUP_MENU_DISPLACEMENT,

         event);

}

</pre>

In this <a name="iddle2653"></a><a name="iddle2654"></a><a name="iddle2655"></a><a name="iddle2656"></a><a name="iddle2657"></a>case, we remember the menu that was generated last time. If we are past it in the same view, and we do not believe that the menu for that view has changed, we just use the same menu that we used last time instead of creating a new one. This is not a sophisticated technique, and it will break down if the user does not open a pop-up menu in the same directory repeatedly. For example, if the user opens a pop-up in directory 1, and then opens one in directory 2, if the user then opens a pop-up in directory 1, nautilus will still create a new menu. It is possible to create a simple cache that stores menus as they are created. When opening a menu, the first check is to see whether these views already have menus in the cache. If they do, the cached menus could be viewed; otherwise, new ones could be created. This cache would be especially useful for some special directories, such as the desktop, computer, or home directory where the user will most likely open a pop-up menu more than once. After applying this proposed solution and timing it with the 100 iterations, the time has dropped to 24.0 seconds. This is a ~20 percent performance improvement, and close to the theoretical improvement that we would get if we did not create the menu at all (21.9 seconds). Creating pop-up menus in various directories worked as expected. The patch did not appear to break anything.

Note, however, that right now, this is just a test solution. It would have to be presented to the nautilus developers to confirm that it did not break any functionality and is suitable for inclusion. However, through the course of the hunt, we have determined what functions are slow, tracked down where they are called, and created a possible solution that objectively improves performance. It is also important to note that the improvement was objective; that is, we have hard data to prove that the new method is faster, rather than simply subjective (i.e., just saying that it feels snappier). Most developers would love to have this <a name="iddle2658"></a><a name="iddle2659"></a><a name="iddle2660"></a><a name="iddle2661"></a><a name="iddle2662"></a>kind of performance bug report.