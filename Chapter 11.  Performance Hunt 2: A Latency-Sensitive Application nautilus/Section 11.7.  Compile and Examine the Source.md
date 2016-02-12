### 11.7\. Compile and Examine the Source

So now that <a name="iddle2570"></a><a name="iddle2571"></a><a name="iddle2572"></a><a name="iddle2573"></a><a name="iddle2574"></a><a name="iddle2575"></a><a name="iddle2576"></a>we have some idea about which calls the application is taking all of the time, we will download the source and compile it. Until now, all of our analysis was possible using the binary packages that Red Hat provides. However, now we need to dive into the source code to examine why the hot functions are called and then, when we figure out why, make changes in the source to alleviate the performance problem. As we did for GIMP, when we recompile, we generate debugging symbols by setting <tt>CFLAGS</tt> to <tt>-g</tt> before we call the configure script.

In this case, we downloaded and installed Red Hat's source <tt>rpm</tt> for nautilus, which places the source of nautilus in <tt>/usr/src/redhat/SOURCES/</tt>. By using Red Hat's source package, we have the exact source and patches that Red Hat used to create the binary in the package. It is important to investigate the source that was used to create the binaries that we have been investigating, because another version may have different performance characteristics. After we extract the source, we can begin to figure out where the <tt>bonobo_window_add_popup</tt> call is made. We can search all the source files in the nautilus directory using the <a name="iddle2577"></a><a name="iddle2578"></a><a name="iddle2579"></a><a name="iddle2580"></a><a name="iddle2581"></a><a name="iddle2582"></a><a name="iddle2583"></a>commands in [Listing 11.9](ch11lev1sec7.html#ch11ex09).

<a name="ch11ex09"></a>

##### Listing 11.9\.

<pre>[nautilus ]$ find -type f | xargs grep bonobo_window_add_popup

./src/file-manager/fm-directory-view.c: bonobo_window_add_popup\

(get_bonobo_window (view), menu, popup_path);

</pre>

Fortunately, it appears as if <tt>bonobo_window_add_popup</tt> is only called from a single function, <tt>create_popup_menu</tt>, as shown in [Listing 11.10](ch11lev1sec7.html#ch11ex10).

<a name="ch11ex10"></a>

##### Listing 11.10\.

<pre>static GtkMenu *create_popup_menu (FMDirectoryView *view,

                              const char *popup_path)

{

   GtkMenu *menu;

   menu = GTK_MENU (gtk_menu_new ());

   gtk_menu_set_screen (menu, gtk_widget_get_screen (GTK_WIDGET (view)));

   gtk_widget_show (GTK_WIDGET (menu));

   bonobo_window_add_popup (get_bonobo_window (view), menu, popup_path);

   g_signal_connect_object (menu, "hide",

                            G_CALLBACK (popup_menu_hidden),

                            G_OBJECT (view),

                            G_CONNECT_SWAPPED);

       return menu;

}

</pre>

In turn, this <a name="iddle2584"></a><a name="iddle2585"></a><a name="iddle2586"></a><a name="iddle2587"></a><a name="iddle2588"></a><a name="iddle2589"></a><a name="iddle2590"></a>function is called by two other functions: <tt>fm_directory_view_pop_up_background_context_menu</tt> and <tt>fm_directory_view_pop_up_selection_context_menu</tt>. By adding a <tt>printf</tt> to each of the functions, we can determine which one is called when we right-click a window. We then recompile nautilus, launch it, and then right-click the background of the window. nautilus prints out <tt>fm_directory_view_pop_up_background_context_menu</tt>, so we know that this is the function that is called when opening a pop-up menu in the background of the window. The source code for this function is shown in [Listing 11.11](ch11lev1sec7.html#ch11ex11).

<a name="ch11ex11"></a>

##### Listing 11.11\.

<pre>void fm_directory_view_pop_up_background_context_menu (FMDirectoryView

*view, GdkEventButton *event)

{

g_assert (FM_IS_DIRECTORY_VIEW (view));

/* Make the context menu items not flash as they

        * update to proper disabled,

 * etc. states by forcing menus to update now.

 */

update_menus_if_pending (view);

eel_pop_up_context_menu

(create_popup_menu (view, FM_DIRECTORY_VIEW_POPUP_PATH_BACKGROUND),

                           EEL_DEFAULT_POPUP_MENU_DISPLACEMENT,

                    EEL_DEFAULT_POPUP_MENU_DISPLACEMENT, event);

}

</pre>

Now that we have narrowed down exactly where the menu pop-ups are created and displayed, we can begin to figure out exactly which pieces are taking all the time and which pieces are ultimately calling the <tt>g_type_check_instance_is_a</tt> function that <tt>oprofile</tt> says is the hot <a name="iddle2591"></a><a name="iddle2592"></a><a name="iddle2593"></a><a name="iddle2594"></a><a name="iddle2595"></a><a name="iddle2596"></a><a name="iddle2597"></a>function.