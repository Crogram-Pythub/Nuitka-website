.. meta::
   :description: Protect your IP with Nuitka and Themida combined with VM technology
   :keywords: python,protection,reverse engineering,vm,Themida,WinLicense

################
 Nuitka Bundles
################

Nuitka can be purchased and used together as a bundle with other
software.

Right now, the offer available is Themida and WinLicense. Both of these
are Oreans products, for which Nuitka Services as an integrator, i.e.
there is a Nuitka plugin that allows additional features in Python code.

.. note::

   WinLicense combines the same protection-level as Themida with the
   power of advanced license control, offering the most powerful and
   flexible technology that allows developers to securely distribute
   trial and registered versions of their applications.

.. note::

   The limitations right now are.

   -  Only works in Windows, for other platforms we are preparing
      alternative bundles.
   -  Only works in Nuitka commercial, in fact Nuitka Themida is a
      superset of Nuitka commercial.

******************
 What is Themida?
******************

Themida is an SDK, where you modify the C code with macros, that when
compiled, end up as DLL usages for a special DLL. In a next step, it
then modifies the created binary and applies VM protection according to
settings and those macros, can be using multiple VMs for different code,
checks for running debugger, etc.

Nuitka Themida adds the ability, to do this directly in the Python code.
Is it not practical to do this manually with Nuitka, as it doesn't
respect things in protection.

**********
 Features
**********

File Embedding
==============

While Nuitka commercial already allows embedding of data files, with
Nuitka Themida it is also possible to embed the CPython DLL, extension
modules, and DLLs used by it into one single binary. That on its own is
making it much harder to attack with file replacements, editing of data
files, but there is still the possibility of switching the DLLs.

With Nuitka Themida your binary is one file exactly, but without the
Nuitka ``--onefile`` binary that unpacks the final executable and DLLs
to a temporary folder, that then does not protect those files. But
Nuitka Themida makes it impossible to access these files.

Enhanced anti-debugger
======================

Nuitka commercial has its own ``anti-debugger`` plugin, currently not
listed as an official feature. But Themida has a more advanced
protection at this time.

C Macros contained in Python code
=================================

This code example using the VM Tiger Red, there is a large variety of
VMs available, with different properties, they all work in the same way
to be activated for a piece of code.

.. code:: python

   def sensitiveCode():

     something_that_prepares_but_is_not_critical
     ...

     # This unused variable is harmless in Python, when compiled with Nuitka it is
     # inserted as C code in the correct spot.
     _inject_c_code = """
        VM_TIGER_RED_START;
        int my_value = 0;
        // Check for effective protection.
        CHECK_PROTECTION(my_value, 1);
        if (my_value != 1) {
           exit(1);
        }

        // Check for debugger.
        CHECK_DEBUGGER(my_value, 2);
        if (my_value != 2) {
           exit(2);
        }
     """

     secret_calculation = ...

     _inject_c_code = """
        VM_TIGER_RED_END;
     """

*****************************************
 All the Power of Themida and WinLicense
*****************************************

Contained in Nuitka Themida is a default configuration, that is used for
building your Python program. The defaults are considered to be good,
but you can choose to edit this by simply executing e.g.

.. code:: bash

   themida.exe .\nuitka\plugins\commercial\ThemidaPlugin\config.tmd

You can then provide your own options. You do not have to configure
anything in terms of includes files, used VMs, etc. Nuitka handles that
all automatically for you, and this for curious and advanced users only.

*********
 Pricing
*********

Oreans charges differently for single develop and team licenses. Also
with WinLicense, you get to use their C API to check license status at a
higher price.

+----------------------+----------------+----------------+----------+
| Product              | Oreans Price   | Nuitka Themida | Combined |
+======================+================+================+==========+
| Themida Developer    | 199            | 500            | 699      |
+----------------------+----------------+----------------+----------+
| Themida Company      | 399            | 500            | 899      |
+----------------------+----------------+----------------+----------+
| WinLicense Developer | 399            | 500            | 899      |
+----------------------+----------------+----------------+----------+
| WinLicense Company   | 799            | 500            | 1299     |
+----------------------+----------------+----------------+----------+

.. note::

   At the price, Nuitka Services cannot handle trial versions.

.. note::

   If you already own a Themida or WinLicense license, you can purchase
   them from Oreans Themida separately.
