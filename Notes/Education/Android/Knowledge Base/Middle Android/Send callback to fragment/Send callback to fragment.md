1 - Interface: 
```Java
public class MyFragment extends Fragment {

    private OnFragmentInteractionListener mListener;

    // Определяем интерфейс
    public interface OnFragmentInteractionListener {
        void onFragmentInteraction(String data);
    }

    @Override
    public void onAttach(Context context) {
        super.onAttach(context);
        if (context instanceof OnFragmentInteractionListener) {
            mListener = (OnFragmentInteractionListener) context;
        } else {
            throw new RuntimeException(context.toString() + " must implement OnFragmentInteractionListener");
        }
    }

    // Вызов callback-а
    private void sendDataToActivity(String data) {
        if (mListener != null) {
            mListener.onFragmentInteraction(data);
        }
    }

    @Override
    public void onDetach() {
        super.onDetach();
        mListener = null;
    }
}
```

2 - Shared View Model

```Java
public class SharedViewModel extends ViewModel {
    private final MutableLiveData<String> selectedItem = new MutableLiveData<>();

    public void selectItem(String item) {
        selectedItem.setValue(item);
    }

    public LiveData<String> getSelectedItem() {
        return selectedItem;
    }
}

public class FirstFragment extends Fragment {

    private SharedViewModel sharedViewModel;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_first, container, false);

        sharedViewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);

        // Передаем данные в ViewModel
        sharedViewModel.selectItem("Hello from FirstFragment");

        return view;
    }
}


public class SecondFragment extends Fragment {

    private SharedViewModel sharedViewModel;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_second, container, false);

        sharedViewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);

        // Подписываемся на изменения данных
        sharedViewModel.getSelectedItem().observe(getViewLifecycleOwner(), item - {
            // Обрабатываем полученные данные
            Toast.makeText(getActivity(), "Received: " + item, Toast.LENGTH_SHORT).show();
        });

        return view;
    }
}
```

3 - Fragment Result API
```Java
///В фрагменте, который передает данные:
Bundle result = new Bundle();
result.putString("bundleKey", "Hello from Fragment A");
getParentFragmentManager().setFragmentResult("requestKey", result);

///В фрагменте, который принимает данные
getParentFragmentManager().setFragmentResultListener("requestKey", this, (requestKey, result) -> {
    String data = result.getString("bundleKey");
    Toast.makeText(getContext(), "Received: " + data, Toast.LENGTH_SHORT).show();
});
```